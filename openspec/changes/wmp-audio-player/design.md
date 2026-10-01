# Design: Windows Media Player Desktop em Streamlit

## Context

Para atender aos requisitos descritos em `proposal.md` sem depender de banco de dados relacional ou infraestrutura de servidor complexa, a aplicação será construída inteiramente em Python 3 utilizando a biblioteca `streamlit` para a camada de interface web/desktop local. A lógica de áudio e gerenciamento de arquivos será organizada em módulos autônomos.

## Goals / Non-Goals

**Goals:**
- Prover uma interface em Streamlit inspirada no visual clássico do Windows Media Player (WMP 11/12) com CSS customizado.
- Garantir importação local e parsing robusto de arquivos MP3 e extração de capas de álbum usando `mutagen`.
- Persistir bibliotecas de mídia e playlists exclusivamente através de arquivos JSON (`storage/library.json` e `storage/playlists.json`).
- Implementar reprodução contínua de áudio, navegação por tempo (seek), controle de volume, modos de repetição (repeat) e ordem aleatória (shuffle).

**Non-Goals:**
- Conectar a serviços de streaming online (como Spotify, YouTube Music ou SoundCloud).
- Suportar formatos de vídeo ou codecs proprietários não suportados por bibliotecas Python de áudio padrão.
- Utilizar bancos de dados relacionais (SQLite, PostgreSQL, MySQL).

## Decisions

### 1. Arquitetura Modular em Camadas
- **Decisão**: Dividir a aplicação em 3 camadas principais:
  1. **Core Engine** (`core/`):
     - `player.py`: Gerenciamento do ciclo de reprodução e estado de áudio (usando `pygame.mixer`).
     - `library.py`: Escaneamento de pastas, leitura de metadados ID3 (`mutagen`), extração de capas e manipulação do `library.json`.
     - `playlist.py`: Lógica de gerenciamento, adição/remoção de músicas e salvar `playlists.json`.
  2. **UI Components** (`ui/`):
     - `components.py`: Componentes modulares do Streamlit para o player WMP (header, barra de controles inferior, visualizador de capa, tabela de faixas).
  3. **Estilização Visual** (`assets/style.css`):
     - Estilos CSS aplicados via `st.markdown(unsafe_allow_html=True)` para redefinir o tema padrão do Streamlit para a estética WMP (tons de azul metálico, transparência, gradientes brilhantes e controles estilizados).

- **Alternativas Consideradas**:
  - *Monolítico em um único arquivo `app.py`*: Rejeitado por dificultar manutenção, legibilidade e testes unitários das regras de negócio.

### 2. Motor de Áudio Local
- **Decisão**: Utilizar `pygame.mixer` para inicialização e controle local de reprodução de áudio MP3 (play, pause, unpause, stop, set_volume, get_pos).
- **Alternativas Consideradas**:
  - *HTML5 `<audio>` nativo no Streamlit*: Possibilita reprodução web nativa, porém não oferece controle contínuo avançado nem eventos síncronos de término de faixa para autorreprodução de playlists sem refresh da página.

### 3. Extração e Armazenamento de Capas de Álbum
- **Decisão**: O módulo `library.py` utiliza `mutagen` para inspecionar frames APIC (Attached Picture) do MP3. Quando presente, a imagem é extraída, convertida via `Pillow` e gravada no diretório `storage/covers/<hash_album>.png`. Quando ausente, é associada uma imagem fallback do WMP.
- **Alternativas Consideradas**:
  - *Armazenar imagens codificadas em string Base64 dentro do próprio `library.json`*: Rejeitado devido ao inchaço excessivo do arquivo JSON.

### 4. Persistência em JSON
- **Decisão**: Arquivos JSON estruturados com indentação:
  - `storage/library.json`: Array de objetos de faixas contendo `id`, `filepath`, `title`, `artist`, `album`, `year`, `genre`, `duration`, `cover_path`.
  - `storage/playlists.json`: Array de objetos de playlists contendo `id`, `name`, `track_ids`, `created_at`.

## Risks / Trade-offs

- **Limitação de Re-rendering do Streamlit**: O Streamlit re-executa o script a cada interação de componente.
  - *Mitigação*: Armazenar todas as variáveis de estado no `st.session_state` (ex: `st.session_state.current_track`, `st.session_state.is_playing`, `st.session_state.playback_pos`) e otimizar callbacks.
- **Formatação de arquivos MP3 corrompidos/sem tags ID3**: Arquivos de áudio sem tags válidas podem quebrar o parser.
  - *Mitigação*: Fallbacks automáticos no parser usando o nome do arquivo físico como título e metadados padrão ("Desconhecido").
