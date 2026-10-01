# Spec Delta

## Purpose

Define a interface visual desktop desenvolvida em Streamlit com estilização CSS personalizada baseada na identidade clássica do Windows Media Player (estética azul/escura, visualizador, painel de capas e controles).

## ADDED Requirements

### Requirement: Layout inspirado no Windows Media Player
O sistema MUST apresentar uma interface em Streamlit estilizada via CSS customizado que simule o layout clássico do Windows Media Player.

#### Scenario: Visualizar painel principal do player
- **WHEN** a aplicação Streamlit é iniciada no navegador
- **THEN** a tela exibe o cabeçalho WMP, área de visualização/capa de álbum, barra lateral de navegação e controles de transporte na parte inferior

### Requirement: Painel de detalhes da faixa atual
O sistema MUST exibir a capa do álbum, título da música, artista, álbum, gênero e tempo decorrido/total da música em execução.

#### Scenario: Atualizar exibição ao mudar de música
- **WHEN** a faixa em reprodução é alterada
- **THEN** o painel visual atualiza a arte da capa e os metadados exibidos instantaneamente

### Requirement: Barra de controles e navegação interativa
O sistema MUST oferecer botões interativos para Play, Pause, Stop, Previous, Next, Mute, Repeat, Shuffle e barra de seek.

#### Scenario: Interagir com controles na interface
- **WHEN** o usuário clica no botão Mute na barra inferior
- **THEN** o áudio é silenciado e o ícone reflete o novo estado de mudo
