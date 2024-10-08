# Versionamento

| Data       | Versão | Descrição | Autor |
|------------|--------|-----------|-------|
| 21/07/2024 | 1.0 | Criação do documento | [Kathlyn Lara Murussi](https://github.com/klmurussi) |
| 21/07/2024 | 1.1 | Adição das tabelas Jogador, Nivel, Inventario, Local e leva | [Kathlyn Lara Murussi](https://github.com/klmurussi) |
| 21/07/2024 | 1.2 | Adição das tabelas Regiao, Clima e Instancia_Item | [Sebastián Zuzunaga](https://github.com/sebazac332) |
| 21/07/2024 | 1.3 | Adição das tabelas que faltam | [Kathlyn Lara Murussi](https://github.com/klmurussi) |

# Dicionário de Dados
São informações sobre os dados que estão sendo utilizados no projeto.

Legenda de Restrições:
- PK: Primary Key
- FK: Foreign Key
- AI: Auto Increment
- NN: Not Null
- UN: Unique

## Tabela: Jogador
Descrição: Tabela que representa o jogador controlado pelo usuário.

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

## Tabela: Inventário
Descrição: Tabela que representa o inventário do jogador.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idInventario | int | PK, AI, NN | Identificador único do inventário |
| idJogador | int | FK, NN | Identificador do jogador |
| pesoMaximo | int | NN | Peso máximo que o jogador pode carregar |
| pesoAtual | int | NN | Peso atual que o jogador está carregando |

## Tabela: Nível
Descrição: Tabela que representa o nível do jogador e suas características.

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

## Tabela: Local
Descrição: Tabela que representa os locais que o jogador pode visitar.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| posX | int | PK, NN | Posição X do local |
| posY | int | PK, NN | Posição Y do local |
| nome | varchar(20) | NN, UN | Nome do local|
| descricao | varchar(100) | NN | Descrição do local |
| reqEntrada | int | FK | Item necessário para entrar no local |
| tipo | char(1) | NN | Tipo do local, 1 - Cidade, 2 - Floresta, 3 - Caverna, 4 - Castelo |
| idRegiao | int | NN, FK | Região onde está o local |

## Tabela: esta
Descrição: Tabela que representa o local em que o jogador está.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idJogador | int | FK, NN | Identificador do jogador |
| posX | int | FK, NN | Posição X do local |
| posY | int | FK, NN | Posição Y do local |

## Tabela: leva
Descrição: um local leva a outro local.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| posXOrigem | int | FK, NN | Posição X do local de origem |
| posYOrigem | int | FK, NN | Posição Y do local de origem |
| posXDestino | int | FK, NN | Posição X do local de destino |
| posYDestino | int | FK, NN | Posição Y do local de destino |

## Tabela: Item
Descrição: Tabela que representa os itens/objetos que o jogador pode adquirir e melhorar seu personagem.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idItem | int | PK, AI, NN | Identificador único do item |
| nome | varchar(20) | NN | Nome do item |
| descricao | varchar(100) | NN | Descrição do item |
| peso | int | NN | Peso do item |
| preco | int | NN | Valor do item para vender ou comprar |

## Tabela: Instancia_Item
Descrição: Tabela que representa as instâncias dos objetos que o jogador pode obter.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| Id | int | PK, AI, NN | Identificador único da instância do objeto |
| idItem | int | FK, NN | Identificador do item |

## Tabela: guarda
Descrição: Tabela que representa os itens que o jogador possui no inventário.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idInventario | int | FK, NN | Identificador do inventário |
| idItem | int | FK, NN | Identificador do item |
| quantidade | int | NN | Quantidade do item no inventário |
| idInstancia_Item | int | FK, NN | Identificador da instância do item |

## Tabela: NaoConsumivel
Descrição: Tabela que representa os itens não consumíveis que o jogador pode equipar.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idItem | int | PK, FK, NN | Identificador único do item |
| estaEquipado | char(1) | NN | Se o item está equipado ou não, 1 - Sim, 2 - Não |

## Tabela: Consumivel
Descrição: Tabela que representa os itens consumíveis que o jogador pode usar. Ou seja, que são removidos do inventário após o uso.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idItem | int | PK, FK, NN | Identificador único do item |

## Tabela: Arma
Descrição: Tabela que representa as armas que o jogador pode equipar e melhorar seu ataque.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idItem | int | PK, FK, NN | Identificador único do item |
| ataqueAdd | int | NN | Valor de ataque que a arma adiciona ao jogador |
| requerForca | int | NN | Valor de força necessário para equipar a arma |

## Tabela: Armadura
Descrição: Tabela que representa as armaduras que o jogador pode equipar e melhorar sua defesa.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idItem | int | PK, FK, NN | Identificador único do item |
| defesaAdd | int | NN | Valor de defesa que a armadura adiciona ao jogador |
| requerConstituicao | int | NN | Valor de constituição necessário para equipar a armadura |

## Tabela: Porcao
Descrição: Tabela que representa as poções que o jogador pode usar para recuperar vida ou mana.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idItem | int | PK, FK, NN | Identificador único do item |
| efeito | char(1) | NN | Efeito da poção, 1 - Vida, 2 - Mana |
| duracao | int | NN | Duração do efeito da poção em turnos |
| multEfeito | int | NN | Multiplicador do efeito da poção |

## Tabela: Acessorio
Descrição: Tabela que representa os acessórios que o jogador pode equipar e melhorar suas características.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idItem | int | PK, FK, NN | Identificador único do item |
| tipo | char(1) | NN | Tipo do acessório, 1 - Anel, 2 - Colar, 3 - Bracelete |
| efeito | char(1) | NN | Efeito do acessório, 1 - Sabedoria, 2 - Força, 3 - Carisma, 4 - Inteligência, 5 - Destreza, 6 - Constituição |
| multEfeito | int | NN | Multiplicador do efeito do acessório |

## Tabela: Magia_Livro
Descrição: Tabela que representa as magias que o jogador pode aprender e usar.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idItem | int | PK, FK, NN | Identificador único do item |
| nome | varchar(20) | NN, PK | Nome da magia |
| descricao | varchar(100) | NN | Descrição da magia |
| manaUtilizada | int | NN | Quantidade de mana que a magia utiliza |
| tipo | char(1) | NN | Tipo da magia, 1 - Ataque, 2 - Defesa, 3 - Cura |
| multEfeito | int | NN | Multiplicador do efeito da magia |
| requerSabedoria | int | NN | Valor de sabedoria necessário para aprender a magia |

## Tabela: Missao
Descrição: Tabela que representa as missões que o jogador pode aceitar e completar.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idMissao | int | PK, AI, NN | Identificador único da missão |
| nome | varchar(20) | NN | Nome da missão |
| descricao | varchar(100) | NN | Descrição da missão |
| recDinheiro | int | NN | Recompensa em dinheiro da missão |
| recExp | int | NN | Recompensa em experiência da missão |
| idNPC | int | FK, NN | Identificador do NPC que deu a missão |

## Tabela: faz
Descrição: Tabela que representa as missões que o jogador pode aceitar e completar.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idJogador | int | FK, NN | Identificador do jogador |
| idMissao | int | FK, NN | Identificador da missão |
| status | char(1) | NN | Status da missão, 1 - Aceita, 2 - Em andamento, 3 - Concluída |

## Tabela: recompensa
Descrição: Tabela que representa as recompensas que o jogador pode receber ao completar uma missão.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idMissao | int | FK, NN | Identificador da missão |
| idItem | int | FK, NN | Identificador do item |
| idInstancia_Item | int | FK, NN | Identificador da instância do item |

## Tabela: NPC
Descrição: Tabela que representa os NPCs que o jogador pode interagir.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idNPC | int | PK, AI, NN | Identificador único do NPC |
| nome | varchar(20) | NN | Nome do NPC |
| raca | char(1) | NN | Raça do NPC, 1 - Humano, 2 - Elfo, 3 - Anão, 4 - Orc |
| sexo | char(1) | NN | Sexo do NPC, 1 - Masculino, 2 - Feminino |

## Tabela: InstanciaNPC
Descrição: Tabela que representa as instâncias dos NPCs que o jogador pode interagir.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| id | int | PK, AI, NN | Identificador único da instância do NPC |
| idNPC | int | FK, NN | Identificador do NPC |

## Tabela: aparece
Descrição: Tabela que representa os NPCs que aparecem em determinados locais.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idNPC | int | FK, NN | Identificador do NPC |
| posX | int | FK, NN | Posição X do local |
| posY | int | FK, NN | Posição Y do local |
| idInstanciaNPC | int | FK, NN | Identificador da instância do NPC |

## Tabela: interage
Descrição: Tabela que representa as interações que o jogador pode ter com os NPCs.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idJogador | int | FK, NN | Identificador do jogador |
| idNPC | int | FK, NN | Identificador do NPC |
| idInstanciaNPC | int | FK, NN | Identificador da instância do NPC |
| texto | varchar(100) | NN | Texto da interação |
| numDialogo | int | NN, PK, AI | Número do diálogo da interação |
| status | char(1) | NN | Status da interação, 1 - Iniciada, 2 - Em andamento, 3 - Concluída |

## Tabela: ProvedorDeMissao
Descrição: Tabela que representa os provedores de missão que o jogador pode interagir.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idNPC | int | PK, FK, NN | Identificador do NPC |

## Tabela: Vendedor
Descrição: Tabela que representa os vendedores que o jogador pode interagir.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idNPC | int | PK, FK, NN | Identificador do NPC |
| dinheiro | int | NN | Quantidade de dinheiro que o vendedor possui |

## Tabela: vende
Descrição: Tabela que representa os itens que o vendedor possui para vender.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idNPC | int | FK, NN | Identificador do NPC |
| idItem | int | FK, NN | Identificador do item |
|idInstancia_Item | int | FK, NN | Identificador da instância do item |

## Tabela: compra
Descrição: Tabela que representa os itens que o jogador comprou do vendedor.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idItem | int | FK, NN | Identificador do item |
| idInstancia_Item | int | FK, NN | Identificador da instância do item |
| idNPC | int | FK, NN | Identificador do NPC |

## Tabela: Inimigo
Descrição: Tabela que representa os inimigos que o jogador pode enfrentar.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idNPC | int | PK, FK, NN | Identificador do NPC |
| vidaMaxima | int | NN | Vida máxima do inimigo |
| vidaAtual | int | NN | Vida atual do inimigo |
| manaMaxima | int | NN | Mana máxima do inimigo |
| defesa | int | NN | Valor da defesa do inimigo |
| ataque | int | NN | Valor do ataque do inimigo |

## Tabela: usa
Descrição: Tabela que representa as magias que o inimigo pode usar.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| idNPC | int | FK, NN | Identificador do NPC |
| magiaNome | varchar(20) | FK, NN | Nome da magia que o inimigo usa |

## Tabela: Clima
Descrição: Tabela que representa o clima que tem a região em que o jogador está.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| Id | int | PK, AI, NN | Identificador única do clima |
| Descricao | varchar(50) | NN | Descrição do clima e dos seus efeitos no ambiente |
| Nome | varchar(20) | NN | Nome do clima que atualmente está na região |
| Tipo_vantagem | char(1) | NN | Aumenta a eficácia de um tipo de magia, 1 - Ataque, 2 - Defesa, 3 - Cura, 4 - Todas, 5 - Nenhuma|
| Tipo_desvantagem | char(1) | NN | Diminuição a eficácia de um tipo de magia, 1 - Ataque, 2 - Defesa, 3 - Cura, 4 - Todas, 5 - Nenhuma |

## Tabela: Regiao
Descrição: Tabela que representa as regiões existentes no jogo.

| Atributo | Tipo | Restrições | Descrição |
|----------|------|------------|-----------|
| Id | int | PK, AI, NN | Identificador única da região |
| idClima | int | FK, NN | Identificação do clima atualmente na região |
| Nome | varchar(20) | NN | Nome da região |
| Descricao | varchar(50) | NN | Descrição das especificidades da região e pontos de interesse |
