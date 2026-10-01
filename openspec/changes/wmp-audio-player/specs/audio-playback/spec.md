# Spec Delta

## Purpose

Gerencia o ciclo de vida da reprodução de áudio, incluindo reprodução, pausa, interrupção, posicionamento de tempo, ajuste de volume e modos de reprodução contínua (repeat e shuffle).

## ADDED Requirements

### Requirement: Reprodução de arquivo de áudio
O sistema MUST carregar e reproduzir arquivos no formato MP3 fornecidos pela biblioteca ou playlist ativa.

#### Scenario: Iniciar reprodução de faixa
- **WHEN** o usuário seleciona uma faixa e aciona o comando Play
- **THEN** o sistema inicia a reprodução do áudio a partir do segundo 0 e atualiza o estado de reprodução para Ativo

#### Scenario: Pausar e retomar reprodução
- **WHEN** o usuário aciona o comando Pause durante a reprodução
- **THEN** o áudio é congelado no segundo atual e a ação subsequente de Play retoma do mesmo ponto

### Requirement: Navegação por posição de tempo (Seek)
O sistema MUST permitir alterar a posição atual de reprodução do áudio através de um seletor ou slider de progresso.

#### Scenario: Alterar tempo de reprodução
- **WHEN** o usuário arrasta o slider de tempo para uma nova posição
- **THEN** o tempo de reprodução atual salta imediatamente para o segundo correspondente selecionado

### Requirement: Modos de reprodução Repeat e Shuffle
O sistema MUST suportar modos de repetição de faixa/playlist e ordem aleatória durante a reprodução da fila.

#### Scenario: Alternar para modo Shuffle
- **WHEN** o modo Shuffle é ativado durante a reprodução de uma playlist
- **THEN** a próxima faixa selecionada ao finalizar a música atual é sorteada aleatoriamente sem repetições consecutivas

#### Scenario: Alternar para modo Repetição
- **WHEN** o modo Repeat está ativo ao alcançar o fim de uma faixa
- **THEN** o sistema reinicia a mesma faixa ou a playlist a partir do início
