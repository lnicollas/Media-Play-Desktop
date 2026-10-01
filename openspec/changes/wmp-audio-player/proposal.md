# Proposal: Windows Media Player Desktop Audio Player em Streamlit

## Why

Atualmente, não existe um player de áudio desktop local desenvolvido em Python com interface Streamlit que combine a facilidade de navegação web com a estética clássica e nostálgica do Windows Media Player. Usuários que buscam organizar e ouvir suas bibliotecas locais de arquivos MP3 necessitam de uma solução leve, sem dependências de bancos de dados relacionais complexos, com suporte a metadados completos (incluindo capas de álbum), gerenciamento flexível de playlists e controles de reprodução avançados.

## What Changes

- **Importação e Varredura de MP3**: Suporte a importação de arquivos MP3 individuais ou pastas locais, com extração automática de tags ID3 (título, artista, álbum, ano, gênero, duração e arte da capa).
- **Biblioteca de Mídia Local**: Organização da biblioteca de áudio persistida em arquivo JSON local, permitindo buscas, filtragens por artista/álbum/gênero e edição de metadados.
- **Gerenciador de Playlists**: Criação, reordenação, edição e exclusão de playlists personalizadas, também salvas no arquivo JSON local.
- **Motor de Reprodução e Controles Avançados**: Controles de play/pause/stop, barra de progresso com busca por tempo (seek), controle de volume, modos de reprodução (repetir faixa/lista e modo aleatório/shuffle).
- **Interface Streamlit Estilizada estilo WMP**: Layout visual rico utilizando CSS customizado e componentes Streamlit inspirados na interface clássica do Windows Media Player (painel de visualização/capa, playlist lateral, barra de controles inferior e cabeçalho de navegação).

## Capabilities

### New Capabilities
- `audio-playback`: Controle de reprodução de áudio, navegação por tempo, volume e modos de repetição/shuffle.
- `media-library`: Varredura, parsing de metadados ID3 (incluindo capas de álbum), armazenamento e gerenciamento da biblioteca local em JSON.
- `playlist-management`: Gestão de playlists personalizadas (criar, editar, ordenar, remover faixas e salvar localmente).
- `wmp-ui-interface`: Interface web/desktop inspirada no Windows Media Player com styling CSS customizado, layout responsivo e controles visuais.

### Modified Capabilities
*(Nenhuma capacidade existente alterada, pois este é um projeto novo)*

## Impact

- **Código e Dependências**: Aplicação desenvolvida em Python (3.9+) utilizando `streamlit`, `pygame` (ou `just_playback`/`PyQt5.QtMultimedia`/`pydub` para execução de áudio), `mutagen` (extração de ID3 tags e imagens), e `Pillow` (processamento de capas de álbum).
- **Persistência**: Armazenamento em arquivos JSON locais (`library.json`, `playlists.json`) e pasta local para cache/armazenamento de capas de álbum decodificadas (`storage/covers/`).
- **Nenhum Banco de Dados Relacional**: Operação 100% autônoma usando arquivos locais JSON para facilitar portabilidade e simplicidade.
