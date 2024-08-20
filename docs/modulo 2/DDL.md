# Versionamento

| Data       | Versão | Descrição | Autor |
|------------|--------|-----------|-------|
| 20/08/2024 | 1.0 | Primeira versão concluída | [Sebastián Zuzunaga](https://github.com/sebazac332) |

# Linguagem de Definição de Dados

Usamos a linguagem de definição de dados (Data Definition Language) para criar as tabelas que irão representar entidades e certas relações entre elas dentro do banco de dados. Também usamos constraints para garantir certas dependências entre dados de diferentes tabelas e para a inserção correta e modificação dos mesmos.

```

CREATE TABLE Jogador (
	id_jogador int AUTO_INCREMENT not null,
    nome varchar(20) not null,
    sexo char(1) not null,
    vidaMaxima int not null,
    vidaAtual int not null,
    manaMaxima int not null,
    manaAtual int not null,
    dinheiro int not null,
    experiencia int not null,
    defensa int not null,
    ataque int not null,
    CONSTRAINT jogador_pk PRIMARY KEY(id_jogador),
	CONSTRAINT sexo_jogador CHECK (tipo IN ('1', '2')),
	CONSTRAINT jogador_positive_values CHECK ( 
		vidaMaxima >= 0 
		AND vidaAtual >= 0 
		AND manaMaxima >= 0 
		AND manaAtual >= 0 
		AND dinheiro >= 0 
		AND experiencia >= 0 
		AND defensa >= 0 
		AND ataque >= 0
	),
	CONSTRAINT jogador_max_valores CHECK (
		vidaMaxima >= vidaAtual AND
		manaMaxima >= manaAtual
	)
); 

CREATE TABLE Inventario (
	id_inventario int AUTO_INCREMENT not null,
    id_jogador int not null,
    pesoMaximo int not null,
    pesoAtual int not null,
    CONSTRAINT inventario_pk PRIMARY KEY(id_inventario),
    CONSTRAINT jogador_fk_inv FOREIGN KEY(id_jogador) REFERENCES Jogador(id_jogador),
    CONSTRAINT chk_inv_valores CHECK (
		pesoMaximo >= 0 AND 
		pesoAtual >= 0
	),
	CONSTRAINT chk_inv_max_valores CHECK (
		pesoMaximo >= pesoAtual
	)
); 

CREATE TABLE guarda (
	idInventario int not null,
    quantidade int not null,
    idInstancia_Item int not null,
    CONSTRAINT guarda_fk_inv FOREIGN KEY(idInventario) REFERENCES Inventario(id_inventario),
    CONSTRAINT guarda_fk_instanciaitem FOREIGN KEY(idInstancia_Item) REFERENCES Instancia_Item(Id),
	CONSTRAINT chk_guarda_valores CHECK (
		quantidade >= 0 
	)
); 

CREATE TABLE Nivel (
	idNivel int AUTO_INCREMENT  not null,
    idJogador int not null,
    expProximo int not null,
    sabedoria int not null,
    forca int not null,
    carisma int not null,
    inteligencia int not null,
    destreza int not null,
    constituicao int not null,
    CONSTRAINT nivel_pk PRIMARY KEY(idNivel),
    CONSTRAINT jogador_fk_nivel FOREIGN KEY(idJogador) REFERENCES Jogador(id_jogador),
	CONSTRAINT chk_nivel_valores CHECK (
		expProximo >= 0 AND
		sabedoria >= 0 AND
		forca >= 0 AND
		carisma >= 0 AND
		inteligencia >= 0 AND
		destreza >= 0 AND
		constituicao >= 0
	)
); 

CREATE TABLE Item (
	idItem int AUTO_INCREMENT not null,
    nome varchar(20) not null,
    descricao varchar(100) not null,
    peso int not null,
    preco int not null,
    CONSTRAINT item_pk PRIMARY KEY(idItem),
	CONSTRAINT chk_item_valores CHECK (
		peso >= 0 AND
		preco >= 0
	)
); 

CREATE TABLE Instancia_Item (
	Id int AUTO_INCREMENT not null,
	idItem int not null,
    CONSTRAINT item_instancia_pk PRIMARY KEY(Id),
    CONSTRAINT item_fk_instancia FOREIGN KEY(idItem) REFERENCES Item(idItem)
); 

CREATE TABLE NaoConsumivel (
	idItem int not null,
	estaEquipado char(1) not null,
    CONSTRAINT item_fk_naocon FOREIGN KEY(idItem) REFERENCES Item(idItem),
	CONSTRAINT estaequipado_naoconsumivel CHECK (estaEquipado IN ('1', '2'));
); 

CREATE TABLE Arma (
	idItem int not null,
    ataqueAdd int not null,
    requerForca int not null,
    CONSTRAINT item_fk_arma FOREIGN KEY(idItem) REFERENCES NaoConsumivel(idItem),
	CONSTRAINT chk_arma_valores CHECK (
		ataqueAdd >= 0 AND
		requerForca >= 0
	)
); 

CREATE TABLE Acessorio (
	idItem int not null,
    tipo char(1) not null,
    efeito char(1) not null,
    multEfeito int not null,
    CONSTRAINT item_fk_acessorio FOREIGN KEY(idItem) REFERENCES NaoConsumivel(idItem),
	CONSTRAINT tipo_acessorio CHECK (tipo IN ('1', '2', '3')),
    CONSTRAINT efeito_acessorio CHECK (efeito IN ('1', '2', '3', '4', '5', '6')),
	CONSTRAINT chk_acessorio_valores CHECK (
		multEfeito >= 0
	)
); 

CREATE TABLE Armadura (
	idItem int not null,
    defesaAdd int not null,
    requerConstituicao int not null,
    CONSTRAINT item_fk_armadura FOREIGN KEY(idItem) REFERENCES NaoConsumivel(idItem),
	CONSTRAINT chk_armadura_valores CHECK (
		defesaAdd >= 0 AND
		requerConstituicao >= 0
	)
); 

CREATE TABLE Consumivel (
	idItem int not null,
    CONSTRAINT item_fk_con FOREIGN KEY(idItem) REFERENCES Item(idItem)
); 

CREATE TABLE Porcao (
	idItem int not null,
    efeito char(1) not null,
    duracao int not null,
    multEfeito int not null,
    CONSTRAINT item_fk_porcao FOREIGN KEY(idItem) REFERENCES Consumivel(idItem),
    CONSTRAINT efeito_porcao CHECK (efeito IN ('1', '2')),
	CONSTRAINT chk_porcao_valores CHECK (
		duracao >= 0 AND
		multEfeito >= 0
	)
); 

CREATE TABLE Magia_Livro (
	idItem int not null,
    nome varchar(20) not null,
    descricao varchar(100) not null,
    manaUtilizada int not null,
    tipo char(1) not null,
    multEfeito int not null,
    requerSabedoria int not null,
    CONSTRAINT magialivro_pk PRIMARY KEY(nome),
    CONSTRAINT item_fk_magialivro FOREIGN KEY(idItem) REFERENCES Consumivel(idItem),
    CONSTRAINT tipo_magialivro CHECK (tipo IN ('1', '2', '3')),
	CONSTRAINT chk_magialivro_valores CHECK (
		manaUtilizada >= 0 AND
		multEfeito >= 0 AND
		requerSabedoria >= 0
	)
);  

CREATE TABLE Clima (
	Id int AUTO_INCREMENT not null,
    Descricao varchar(50) not null,
    Nome varchar(20) not null,
    Tipo_vantagem char(1) not null,
    Tipo_desvantagem char(1) not null,
    CONSTRAINT clima_pk PRIMARY KEY(Id),
    CONSTRAINT tipo_vantagem_clima CHECK (Tipo_vantagem IN ('1', '2', '3', '4', '5')),
    CONSTRAINT tipo_desvantagem_clima CHECK (Tipo_desvantagem IN ('1', '2', '3', '4', '5'))
);  

CREATE TABLE Regiao (
	Id int AUTO_INCREMENT not null,
    idClima int not null,
    Nome varchar(20) not null,
    Descricao varchar(50) not null,
    CONSTRAINT regiao_pk PRIMARY KEY(Id),
    CONSTRAINT regiao_fk_clima FOREIGN KEY(idClima) REFERENCES Clima(Id)
); 

CREATE TABLE Local (
	posX int not null,
    posY int not null,
    Nome varchar(20) not null,
    descricao varchar(100) not null,
    reqEntrada int,
    tipo char(1) not null,
    idRegiao int not null,
    CONSTRAINT local_pk PRIMARY KEY(posX, posY),
    CONSTRAINT local_fk_item FOREIGN KEY(reqEntrada) REFERENCES Item(idItem),
    CONSTRAINT local_fk_regiao FOREIGN KEY(idRegiao) REFERENCES Regiao(Id),
    CONSTRAINT tipo_local CHECK (tipo IN ('1', '2', '3', '4'))
); 

CREATE TABLE leva (
	posXOrigem int not null,
    posYOrigem int not null,
    posXDestino int not null,
    posYDestino int not null,
    CONSTRAINT leva_fk_origem FOREIGN KEY(posXOrigem, posYOrigem) REFERENCES Local(posX, posY),
    CONSTRAINT leva_fk_destino FOREIGN KEY(posXDestino, posYDestino) REFERENCES Local(posX, posY)
); 

CREATE TABLE esta (
	idJogador int not null,
    posX int not null,
    posY int not null,
    CONSTRAINT esta_fk_jogador FOREIGN KEY(idJogador) REFERENCES Jogador(id_jogador),
    CONSTRAINT esta_fk_local FOREIGN KEY(posX, posY) REFERENCES Local(posX, posY)
); 

CREATE TABLE NPC (
	idNPC int AUTO_INCREMENT not null,
    nome varchar(20) not null,
    raca char(1) not null,
    sexo char(1) not null,
    CONSTRAINT npc_pk PRIMARY KEY(idNPC),
	CONSTRAINT raca_npc CHECK (raca IN ('1', '2', '3', '4')),
    CONSTRAINT sexo_npc CHECK (raca IN ('1', '2'))
); 

CREATE TABLE ProvedorDeMissao (
    idNPC int not null,
	CONSTRAINT provedormissao_fk_npc FOREIGN KEY(idNPC) REFERENCES NPC(idNPC)
); 

CREATE TABLE Vendedor (
    idNPC int not null,
    dinheiro int not null,
	CONSTRAINT vendedor_fk_npc FOREIGN KEY(idNPC) REFERENCES NPC(idNPC),
	CONSTRAINT chk_vendedor_valores CHECK (
		dinheiro >= 0
	)
); 

CREATE TABLE Inimigo (
    idNPC int not null,
    vidaMaxima int not null,
    vidaAtual int not null,
    manaMaxima int not null,
    defesa int not null,
    ataque int not null,
	CONSTRAINT inimigo_fk_npc FOREIGN KEY(idNPC) REFERENCES NPC(idNPC),
	CONSTRAINT chk_inimigo_valores CHECK (
		vidaMaxima >= 0 AND
		vidaAtual >= 0 AND
		manaMaxima >= 0 AND
		defesa >= 0 AND
		ataque >= 0
	),
	CONSTRAINT chk_inimigo_maxvalores CHECK (
		vidaMaxima >= vidaAtual
	)
); 

CREATE TABLE InstanciaNPC (
	id int AUTO_INCREMENT not null,
    idNPC int not null,
    CONSTRAINT instancianpc_pk PRIMARY KEY(id),
	CONSTRAINT instancianpc_fk_npc FOREIGN KEY(idNPC) REFERENCES NPC(idNPC)
); 

CREATE TABLE aparece (
    posX int not null,
    posY int not null,
    idInstanciaNPC int not null,
	CONSTRAINT aparece_fk_instancianpc FOREIGN KEY(idInstanciaNPC) REFERENCES InstanciaNPC(id),
    CONSTRAINT aparece_fk_local FOREIGN KEY(posX, posY) REFERENCES Local(posX, posY)
); 

CREATE TABLE interage (
    idJogador int not null,
    idInstanciaNPC int not null,
    texto varchar(100) not null,
    numDialogo int AUTO_INCREMENT not null,
    status int not null,
    CONSTRAINT interage_pk PRIMARY KEY(numDialogo),
	CONSTRAINT interage_fk_jogador FOREIGN KEY(idJogador) REFERENCES Jogador(id_jogador),
    CONSTRAINT interage_fk_instancianpc FOREIGN KEY(idInstanciaNPC) REFERENCES InstanciaNPC(id),
	CONSTRAINT interage_status CHECK (status IN ('1', '2', '3'))
); 

CREATE TABLE usa (
    idNPC int not null,
    magiaNome varchar(20) not null,
	CONSTRAINT inimigomagia_fk_npc FOREIGN KEY(idNPC) REFERENCES Inimigo(idNPC),
    CONSTRAINT inimigomagia_fk_magia FOREIGN KEY(magiaNome) REFERENCES Magia_Livro(nome)
); 

CREATE TABLE vende (
    idNPC int not null,
    idInstancia_Item int not null,
	CONSTRAINT vende_fk_npc FOREIGN KEY(idNPC) REFERENCES Vendedor(idNPC),
    CONSTRAINT vende_fk_instanciaitem FOREIGN KEY(idInstancia_Item) REFERENCES Instancia_Item(Id)
); 

CREATE TABLE compra (
    idNPC int not null,
    idInstancia_Item int not null,
	CONSTRAINT compra_fk_npc FOREIGN KEY(idNPC) REFERENCES Vendedor(idNPC),
    CONSTRAINT compra_fk_instanciaitem FOREIGN KEY(idInstancia_Item) REFERENCES Instancia_Item(Id)
); 

CREATE TABLE Missao (
    idMissao int AUTO_INCREMENT not null,
    nome varchar(20) not null,
    descricao varchar(100) not null,
    recDinheiro int not null,
    recExp int not null,
    idNPC int not null,
    CONSTRAINT missao_pk PRIMARY KEY(idMissao),
	CONSTRAINT missao_fk_npc FOREIGN KEY(idNPC) REFERENCES ProvedorDeMissao(idNPC),
	CONSTRAINT chk_missao_valores CHECK (
		recDinheiro >= 0 AND
		recExp >= 0
	)
); 

CREATE TABLE recompensa (
    idMissao int not null,
    idInstancia_Item int not null,
    CONSTRAINT recompensa_fk_missao FOREIGN KEY(idMissao) REFERENCES Missao(idMissao),
	CONSTRAINT recompensa_fk_instanciaitem FOREIGN KEY(idInstancia_Item) REFERENCES Instancia_Item(Id)
); 

CREATE TABLE faz (
    idJogador int not null,
    idMissao int not null,
    status char(1) not null,
    CONSTRAINT faz_fk_jogador FOREIGN KEY(idJogador) REFERENCES Jogador(id_jogador),
	CONSTRAINT faz_fk_missao FOREIGN KEY(idMissao) REFERENCES Missao(idMissao),
    CONSTRAINT status_missao CHECK (status IN ('1', '2', '3'))
); 

```