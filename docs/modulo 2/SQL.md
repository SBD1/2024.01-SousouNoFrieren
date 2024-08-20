# Versionamento

| Data       | Versão | Descrição | Autor |
|------------|--------|-----------|-------|
| 20/08/2024 | 1.0 | Primeira versão concluída | [Sebastián Zuzunaga](https://github.com/sebazac332) |

```
-- Visualizar arma, suas estatísticas e quantidade existente
SELECT DISTINCT 
    Item.nome, 
    Item.descricao, 
    Item.peso, 
    Arma.ataqueAdd,
    Arma.requerForca,
    COUNT(Instancia_Item.Id) AS quantidade 
FROM 
    Item 
JOIN 
    Arma ON Item.idItem = Arma.idItem 
JOIN 
    Instancia_Item ON Item.idItem = Instancia_Item.idItem 
GROUP BY 
    Item.nome, Item.descricao, Item.peso, Arma.ataqueAdd, Arma.requerForca;
	
--Ver o status do jogador e onde ele está
SELECT DISTINCT 
    Jogador.nome,
    Jogador.vidaMaxima,
    Jogador.vidaAtual,
    Jogador.manaMaxima,
    Jogador.manaAtual, 
    Local.nome
FROM 
    Jogador 
JOIN 
    esta ON Jogador.id_jogador = esta.idJogador 
JOIN 
    Local ON esta.posX = Local.posX AND esta.posY = Local.posY
GROUP BY 
    Jogador.nome, Jogador.vidaMaxima, Jogador.vidaAtual, Jogador.manaMaxima, Jogador.manaAtual, Local.nome;
	
--Visualizar missão, status da missão, quem está realizando a missão e a recompensa
SELECT 
    Jogador.nome AS jogador,
    Missao.nome AS missao,
    faz.status,
    Missao.recDinheiro AS recompensadinheiro,
    Missao.recExp AS recompensaXP,
    Item.nome AS recompensa
FROM 
    Jogador 
JOIN 
    faz ON Jogador.id_jogador = faz.idJogador 
JOIN 
    Missao ON Missao.idMissao = faz.idMissao
JOIN 
    recompensa ON recompensa.idMissao = Missao.idMissao
JOIN 
    Instancia_Item ON recompensa.idInstancia_Item = Instancia_Item.Id
JOIN
	Item ON Instancia_Item.idItem = Item.idItem
GROUP BY 
    Jogador.nome, Missao.nome, faz.status, Missao.recDinheiro,  Missao.recExp, Item.nome;
	
--Visualizar os inimigos, suas estatísticas e a quantidade de inimigos existentes
SELECT DISTINCT
    NPC.nome,
    Inimigo.vidaMaxima,
    Inimigo.vidaAtual,
    Inimigo.manaMaxima,
    Inimigo.defesa,
    Inimigo.ataque,
    count(InstanciaNPC.id) as quantidade
FROM 
    NPC 
JOIN 
    InstanciaNPC ON InstanciaNPC.idNPC = NPC.idNPC 
JOIN 
    Inimigo ON Inimigo.idNPC = NPC.idNPC
GROUP BY 
    NPC.nome, Inimigo.vidaMaxima, Inimigo.vidaAtual, Inimigo.manaMaxima, Inimigo.defesa, Inimigo.ataque;

--Visualizar itens que cada jogador possui e a quantidade que eles possuem
SELECT DISTINCT
    Item.nome,
	Jogador.nome,
    guarda.quantidade
FROM 
    Item 
JOIN 
    Instancia_Item ON Instancia_Item.idItem = Item.idItem
JOIN
	guarda ON guarda.idInstancia_Item = Instancia_Item.Id
JOIN
	Inventario ON Inventario.id_inventario = guarda.idInventario
JOIN
	Jogador ON Jogador.id_jogador = Inventario.id_jogador
GROUP BY 
    Item.nome, Jogador.nome, guarda.quantidade;

--Visualizar que magias pode usar cada jogador
SELECT DISTINCT
	Jogador.nome AS Jogador,
    Magia_Livro.nome AS Magia_disponivel
FROM 
    Jogador 
JOIN 
    Nivel ON Nivel.idJogador = Jogador.id_jogador
JOIN
	Magia_Livro ON Nivel.sabedoria >= Magia_Livro.requerSabedoria
GROUP BY 
    Jogador.nome, Magia_Livro.nome;

```