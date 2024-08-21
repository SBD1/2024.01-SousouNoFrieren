# Versionamento

| Data       | Versão | Descrição | Autor |
|------------|--------|-----------|-------|
| 20/08/2024 | 1.0 | Primeira versão concluída | [Sebastián Zuzunaga](https://github.com/sebazac332) |

# Linguagem de Manipulação de Dados

A linguagem de manipulação de dados (Data Manipulation Language) é usada para trabalhar com os dados que irão dentro das tabelas, este nos permite inserir novos dados, modificar dados já existentes e eliminar dados que não são mais necessários.

```

INSERT INTO Jogador (nome, sexo, vidaMaxima, vidaAtual, manaMaxima, manaAtual, dinheiro, experiencia, defensa, ataque) VALUES
('John', '1', 100, 100, 50, 50, 100, 0, 10, 10),
('Jane', '2', 100, 100, 50, 50, 100, 0, 10, 10),
('Alex', '1', 100, 100, 50, 50, 100, 0, 10, 10);

INSERT INTO Inventario (id_jogador, pesoMaximo, pesoAtual)
VALUES 
(1, 250, 0),
(2, 250, 0),
(3, 250, 0);

INSERT INTO Nivel (idJogador, expProximo, sabedoria, forca, carisma, inteligencia, destreza, constituicao)
VALUES 
(1, 50, 10, 10, 10, 10, 10, 10),
(2, 50, 10, 10, 10, 10, 10, 10),
(3, 50, 10, 10, 10, 10, 10, 10);

INSERT INTO Item (nome, descricao, peso, preco)
VALUES 
('Espada', 'Uma espada afiada.', 30, 150),
('Armadura', 'Armadura resistente.', 50, 300),
('Poção de Cura', 'Poção que restaura a saúde.', 10, 50),
('Poção de mana', 'Poção que restaura mana.', 10, 50),
('Anel', 'Anel que aumenta as estatísticas.', 20, 250),
('Colar', 'Colar que aumenta as estatísticas.', 20, 250),
('Bracelete', 'Bracelete que aumenta as estatísticas.', 20, 250),
('Grimório de fogo', 'Grimório que contém um feitiço de fogo.', 40, 500),
('Grimório de cura', 'Grimório que contém um feitiço de cura.', 40, 500),
('Grimório de Defesa', 'Grimório que contém um feitiço de defensa.', 40, 500);

INSERT INTO NaoConsumivel (idItem, estaEquipado)
VALUES 
(1,'2'),
(2,'2'),
(5,'2'),
(6,'2'),
(7,'2');

INSERT INTO Consumivel (idItem)
VALUES 
(3),
(4),
(8),
(9),
(10);

INSERT INTO Arma (idItem, ataqueAdd, requerForca)
VALUES 
(1, 25, 15);

INSERT INTO Armadura (idItem, defesaAdd, requerConstituicao)
VALUES 
(2, 25, 15);

INSERT INTO Acessorio (idItem, tipo, efeito, multEfeito)
VALUES 
(5, 1, 5, 1),
(6, 2, 1, 2),
(7, 3, 2, 1.5);

INSERT INTO Porcao (idItem, efeito, duracao, multEfeito)
VALUES 
(3, 1, 5, 15),
(4, 2, 5, 15);

INSERT INTO Magia_Livro (idItem, nome, descricao, manaUtilizada, tipo, multEfeito, requerSabedoria)
VALUES 
(8, 'bola de fogo', 'Bola de fogo que faz dano', 5, 1, 25, 20),
(9, 'Cura menor', 'Regenera uma pequena quantidade de saúde', 15, 3, 20, 25),
(10, 'Proteção inferior', 'Cria uma barreira que diminui ligeiramente o dano recebido', 15, 2, 20, 30);

INSERT INTO Instancia_Item (idItem)
VALUES 
(1),
(1),
(2),
(2),
(5),
(5),
(3),
(4),
(8),
(8),
(9),
(10);

INSERT INTO NPC (nome, raca, sexo)
VALUES 
('Mark', '2', '1'),
('Vendedora', '2', '2'),
('Inimigo', '1', '1');

INSERT INTO ProvedorDeMissao (idNPC)
VALUES 
(1);

INSERT INTO Vendedor (idNPC, dinheiro)
VALUES 
(2, 250);

INSERT INTO Inimigo (idNPC, vidaMaxima, vidaAtual, manaMaxima, defesa, ataque)
VALUES 
(3, 120, 120, 50, 20, 25);

INSERT INTO InstanciaNPC (idNPC)
VALUES 
(1),
(2),
(2),
(3),
(3),
(3);

INSERT INTO Missao (nome, descricao, recDinheiro, recExp, idNPC)
VALUES 
('Missao teste', 'Eliminar 3 inimigos', 50, 20, 1),
('Missao teste 2', 'Obter 1 espada', 100, 40, 1);

INSERT INTO usa (idNPC, magiaNome)
VALUES 
(3, 'bola de fogo');

INSERT INTO vende (idNPC, idInstancia_Item, idItem)
VALUES 
(2, 8, 4),
(2, 3, 2);

INSERT INTO compra (idNPC, idInstancia_Item, idItem)
VALUES 
(2, 10, 8),
(2, 11, 9),
(2, 12, 10);

INSERT INTO recompensa (idMissao, idInstancia_Item, idItem)
VALUES 
(1, 11, 9),
(2, 12, 10);

INSERT INTO guarda (idInventario, quantidade, idInstancia_Item, idItem)
VALUES 
(1, 1, 2, 1),
(2, 1, 5, 5);

INSERT INTO faz (idJogador, idMissao, status)
VALUES 
(1, 1, 1),
(2, 2, 2);

INSERT INTO interage (idJogador, idInstanciaNPC, idNPC, texto, status)
VALUES 
(1, 1, 1, 'Oi, bom dia', 1),
(2, 3, 2, 'Oi boa tarde', 1);

INSERT INTO Clima (Descricao, Nome, Tipo_vantagem, Tipo_desvantagem)
VALUES 
('Grandes quantidades de água caindo do céu', 'chuva', 3, 1),
('Clima seco, falta de água em toda a região', 'Seca', 2, 3),
('Ventos fortes e trovões', 'Tempestade', 5, 1);

INSERT INTO Regiao (idClima, Nome, Descricao)
VALUES 
(1, 'Regiao_teste_1', 'Região inicial, planícies com muita vegetação'),
(3, 'Regiao_teste_2', 'Região montanhosa de tempestades permanentes');

INSERT INTO Local (posX, posY, Nome, descricao, reqEntrada, tipo, idRegiao)
VALUES 
(0, 0, 'Spawn', 'Onde o jogador começa', null, 2, 1),
(0, 1, 'Entrada na floresta', 'Entrada para uma floresta frondosa', null, 2, 1),
(1, 0, 'Caminho da cidade', 'Início de uma estrada que leva à cidade inicial', null, 2, 1),
(1, 1, 'Lagoa', 'Pequena lagoa, conecta entrada com a estrada', null, 2, 1),
(0, 2, 'Sala do inimigo', 'Alguns inimigos aparecem aqui', null, 2, 1),
(2, 0, 'Metade do caminho', 'Parte do caminho que leva ao povo', null, 2, 1),
(2, 1, 'Sala de Mark', 'Aqui está o Mark', null, 2, 1),
(1, 2, 'Sala da árvore', 'Aqui há uma grande árvore', null, 2, 1),
(2, 2, 'Aldeia inicial', 'Primeira cidade que o jogador encontrou', null, 1, 1);

INSERT INTO leva (posXOrigem, posYOrigem, posXDestino, posYDestino)
VALUES 
(0, 0, 0, 1),
(0, 0, 1, 0),
(0, 1, 1, 1),
(0, 1, 0, 0),
(0, 1, 0, 2),
(0, 2, 0, 1),
(0, 2, 1, 2),
(1, 2, 0, 2),
(1, 0, 2, 0),
(1, 0, 1, 1),
(1, 0, 0, 0),
(1, 1, 1, 0),
(1, 1, 0, 1),
(1, 1, 1, 0),
(2, 0, 2, 1),
(2, 1, 2, 0),
(2, 0, 2, 2),
(2, 2, 2, 0);

INSERT INTO esta (idJogador, posX, posY)
VALUES 
(1, 0, 0),
(2, 0, 0),
(3, 1, 0);

INSERT INTO aparece (posX, posY, idInstanciaNPC, idNPC)
VALUES 
(0, 2, 4, 3),
(0, 2, 5, 3),
(0, 2, 6, 3),
(2, 1, 1, 1),
(2, 2, 2, 2),
(2, 2, 3, 2);

```