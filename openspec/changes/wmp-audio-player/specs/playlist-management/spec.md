# Spec Delta

## Purpose

Fornece funcionalidades para criação, manipulação de ordem, adição/remoção de faixas e persistência local de playlists personalizadas pelo usuário.

## ADDED Requirements

### Requirement: Gestão de Playlists
O sistema MUST permitir criar novas playlists, renomeá-las e removê-las.

#### Scenario: Criar nova playlist
- **WHEN** o usuário digita o nome de uma nova playlist e confirma
- **THEN** uma playlist vazia é criada e listada na interface

### Requirement: Manipulação de faixas na playlist
O sistema MUST permitir adicionar faixas da biblioteca para uma playlist existente e reordenar ou remover faixas da fila.

#### Scenario: Adicionar faixa à playlist
- **WHEN** o usuário seleciona uma faixa da biblioteca e adiciona a uma playlist existente
- **THEN** a faixa é inclusa ao final da lista da playlist selecionada

#### Scenario: Remover faixa da playlist
- **WHEN** o usuário remove uma faixa de uma playlist
- **THEN** a faixa é excluída da playlist mantendo o arquivo físico e a biblioteca original intatos

### Requirement: Persistência de playlists em JSON
O sistema MUST salvar a relação e ordenação das playlists no arquivo local `playlists.json`.

#### Scenario: Salvar estado das playlists
- **WHEN** qualquer alteração de playlist é realizada pelo usuário
- **THEN** o arquivo `playlists.json` é atualizado no disco
