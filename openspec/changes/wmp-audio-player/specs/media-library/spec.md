# Spec Delta

## Purpose

Gerencia a verificação de arquivos locais MP3, extração e edição de metadados ID3, capas de álbuns e persistência da biblioteca de mídia em formato JSON.

## ADDED Requirements

### Requirement: Importação e indexação de arquivos MP3
O sistema MUST importar arquivos MP3 locais de diretórios selecionados pelo usuário e extrair metadados ID3 completos.

#### Scenario: Importação de diretório local com MP3s
- **WHEN** o usuário informa o caminho de um diretório com arquivos MP3
- **THEN** o sistema lê cada arquivo, extrai as tags ID3 (Título, Artista, Álbum, Ano, Gênero, Duração) e adiciona os itens à biblioteca

### Requirement: Extração e armazenamento de arte de capa de álbum
O sistema MUST extrair a imagem de capa embutida no arquivo MP3 ou utilizar uma imagem padrão quando inexistente, salvando no storage local.

#### Scenario: Processar faixa com capa embutida
- **WHEN** o arquivo MP3 possui arte de capa na tag ID3 APIC
- **THEN** o sistema extrai a imagem, salva a cópia no armazenamento local e associa o caminho à faixa na biblioteca

### Requirement: Persistência local em JSON sem banco relacional
O sistema MUST salvar a estrutura inteira de dados da biblioteca em um arquivo JSON local chamado `library.json`.

#### Scenario: Salvar dados da biblioteca
- **WHEN** uma nova música é importada ou metadados são alterados
- **THEN** o sistema serializa e grava as atualizações no arquivo `library.json` mantendo a consistência do estado
