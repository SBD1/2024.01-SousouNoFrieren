# Versionamento

| Data       | Versão | Descrição | Autor |
|------------|--------|-----------|-------|
| 21/07/2024 | 1.0 | Criação do documento | [Kathlyn Lara Murussi](https://github.com/klmurussi) |
| 21/07/2024 | 1.1 | Adição das tabelas Jogador, Nivel, Inventario, Local e leva | [Kathlyn Lara Murussi](https://github.com/klmurussi) |

# Dicionário de Dados
São informações sobre os dados que estão sendo utilizados no projeto.

Legenda de Restrições:
- PK: Primary Key
- FK: Foreign Key
- AI: Auto Increment
- NN: Not Null
- UN: Unique

## Entidade: Jogador
Descrição: Entidade que representa o jogador controlado pelo usuário.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idJoagdor | int | PK, AI, NN | Identificador único do jogador |
| nome | varchar(20) | NN |  Nome do jogador, de 3 a 20 letras |
| sexo | char(1) | NN | Sexo do jogador, 1 - Masculino, 2 - Feminino |
| vidaMaxima | int | NN | Vida máxima do jogador |
| vidaAtual | int | NN | Vida atual do jogador |
| manaMaxima | int | NN | Mana máxima do jogador |
| manaAtual | int | NN | Mana atual do jogador |
| dinheiro | int | NN | Quantidade de dinheiro do jogador |
| experiencia | int | NN | Quantidade de experiência do jogador |
| defesa | int | NN | Valor da defesa sem equipamentos |
| ataque | int | NN | Valor do ataque sem equipamentos |

## Entidade: Inventário
Descrição: Entidade que representa o inventário do jogador.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idInventario | int | PK, AI, NN | Identificador único do inventário |
| idJogador | int | FK, NN | Identificador do jogador |
| pesoMaximo | int | NN | Peso máximo que o jogador pode carregar |
| pesoAtual | int | NN | Peso atual que o jogador está carregando |

## Entidade: Nível
Descrição: Entidade que representa o nível do jogador e suas características.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idNivel | int | PK, AI, NN | Identificador único do nível |
| idJogador | int | FK, NN | Identificador do jogador |
| expProximo | int | NN | Quantidade de experiência necessária para o próximo nível |
| sabedoria | int | NN | Valor da sabedoria do jogador |
| forca | int | NN | Valor da força do jogador |
| carisma | int | NN | Valor do carisma do jogador |
| inteligencia | int | NN | Valor da inteligência do jogador |
| destreza | int | NN | Valor da destreza do jogador |
| constituicao | int | NN | Valor da constituição do jogador |

## Entidade: Local
Descrição: Entidade que representa os locais que o jogador pode visitar.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| posX | int | PK, NN | Posição X do local |
| posY | int | PK, NN | Posição Y do local |
| nome | varchar(20) | NN, UN | Nome do local|
| descricao | varchar(100) | NN | Descrição do local |
| reqEntrada | ??? | NN | Requisitos para entrar no local, como nível, itens, etc. |
| tipo | char(1) | NN | Tipo do local, 1 - Cidade, 2 - Floresta, 3 - Caverna, 4 - Castelo |

## Relacionamento: leva
Descrição: um local leva a outro local.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| posXOrigem | int | FK, NN | Posição X do local de origem |
| posYOrigem | int | FK, NN | Posição Y do local de origem |
| posXDestino | int | FK, NN | Posição X do local de destino |
| posYDestino | int | FK, NN | Posição Y do local de destino |



