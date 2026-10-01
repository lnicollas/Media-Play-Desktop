# Tasks: Windows Media Player Desktop em Streamlit

## 1. Estrutura do Projeto e Dependências

- [x] 1.1 Criar o arquivo `requirements.txt` com as dependências `streamlit`, `pygame`, `mutagen`, `Pillow` e verificar que a instalação completa sem erros.
- [x] 1.2 Criar a estrutura de diretórios do projeto (`core/`, `ui/`, `assets/`, `storage/`, `storage/covers/`) e verificar a existência das pastas.

## 2. Biblioteca de Mídia e Persistência JSON

- [x] 2.1 Criar o módulo `core/library.py` com funções para parsing de tags ID3 de arquivos MP3 utilizando `mutagen` (título, artista, álbum, ano, gênero, duração) e verificar extração com arquivos de teste.
- [x] 2.2 Implementar a extração e salvamento da arte de capa do álbum para `storage/covers/` (com suporte a imagem fallback padrão quando ausente) e verificar a gravação do arquivo de imagem.
- [x] 2.3 Implementar a persistência da biblioteca de mídia em `storage/library.json` e a funcionalidade de varredura de diretórios locais.

## 3. Gerenciamento de Playlists

- [x] 3.1 Criar o módulo `core/playlist.py` com funções para criação, edição, renomeação, adição/remoção de faixas e reorganização de playlists.
- [x] 3.2 Implementar a persistência e carregamento das playlists no arquivo `storage/playlists.json` e verificar a correta leitura/escrita do JSON.

## 4. Motor de Reprodução de Áudio (Playback Engine)

- [x] 4.1 Criar o módulo `core/player.py` abstraindo o `pygame.mixer` para controlar operações de Play, Pause, Resume, Stop, ajuste de Volume e Seek de tempo.
- [x] 4.2 Implementar a lógica dos modos de reprodução Repeat (faixa única ou playlist inteira) e Shuffle (ordem aleatória) e verificar o comportamento da fila de reprodução.

## 5. Interface Streamlit e Estilização Windows Media Player

- [x] 5.1 Criar o arquivo CSS `assets/style.css` aplicando a paleta visual clássica azul e prateada do Windows Media Player (estilo gloss, botões metálicos, sombras e visualizador).
- [x] 5.2 Criar o módulo `ui/components.py` com componentes Streamlit estilizados para a barra de transporte inferior, painel de capa de álbum/detalhes, tabela de músicas e menu lateral.
- [x] 5.3 Implementar a aplicação principal em `app.py`, conectando o `st.session_state`, a barra de controles e a navegação entre as views "Tocando Agora", "Biblioteca", "Playlists" e "Importar Mídias".

## 6. Verificação de Integração

- [x] 6.1 Executar a aplicação com `streamlit run app.py` e validar a importação de faixas MP3, criação de playlists, exibição das capas de álbum e controles de reprodução completos (play, pause, seek, volume, repeat e shuffle).
