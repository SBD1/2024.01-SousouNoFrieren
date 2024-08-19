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

```