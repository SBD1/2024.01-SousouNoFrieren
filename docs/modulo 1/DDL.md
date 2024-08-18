```

CREATE TABLE Jogador (
	id_jogador int not null,
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
    CONSTRAINT jogador_pk PRIMARY KEY(id_jogador)
); 

CREATE TABLE Inventario (
	id_inventario int not null,
    id_jogador int not null,
    pesoMaximo int not null,
    pesoAtual int not null,
    CONSTRAINT inventario_pk PRIMARY KEY(id_inventario),
    CONSTRAINT jogador_fk_inv FOREIGN KEY(id_jogador) REFERENCES Jogador(id_jogador)
); 

CREATE TABLE guarda (
	idInventario int not null,
    quantidade int not null,
    idInstancia_Item int not null,
    CONSTRAINT guarda_fk_inv FOREIGN KEY(idInventario) REFERENCES Inventario(id_inventario),
    CONSTRAINT guarda_fk_instanciaitem FOREIGN KEY(idInstancia_Item) REFERENCES Instancia_Item(Id)
); 

CREATE TABLE Nivel (
	idNivel int not null,
    idJogador int not null,
    expProximo int not null,
    sabedoria int not null,
    forca int not null,
    carisma int not null,
    inteligencia int not null,
    destreza int not null,
    constituicao int not null,
    CONSTRAINT nivel_pk PRIMARY KEY(idNivel),
    CONSTRAINT jogador_fk_nivel FOREIGN KEY(idJogador) REFERENCES Jogador(id_jogador)
); 

CREATE TABLE Item (
	idItem int not null,
    nome varchar(20) not null,
    descricao varchar(100) not null,
    peso int not null,
    preco int not null,
    CONSTRAINT item_pk PRIMARY KEY(idItem)
); 

CREATE TABLE Instancia_Item (
	Id int not null,
	idItem int not null,
    CONSTRAINT item_instancia_pk PRIMARY KEY(Id),
    CONSTRAINT item_fk_instancia FOREIGN KEY(idItem) REFERENCES Item(idItem)
); 

CREATE TABLE NaoConsumivel (
	idItem int not null,
	estaEquipado char(1) not null,
    CONSTRAINT item_fk_naocon FOREIGN KEY(idItem) REFERENCES Item(idItem)
); 

CREATE TABLE Arma (
	idItem int not null,
    ataqueAdd int not null,
    requerForca int not null,
    CONSTRAINT item_fk_arma FOREIGN KEY(idItem) REFERENCES NaoConsumivel(idItem)
); 

CREATE TABLE Acessorio (
	idItem int not null,
    tipo char(1) not null,
    efeito char(1) not null,
    multEfeito int not null,
    CONSTRAINT item_fk_acessorio FOREIGN KEY(idItem) REFERENCES NaoConsumivel(idItem),
	CONSTRAINT tipo_acessorio CHECK (tipo IN ('1', '2', '3')),
    CONSTRAINT efeito_acessorio CHECK (efeito IN ('1', '2', '3', '4', '5', '6'))
); 

CREATE TABLE Armadura (
	idItem int not null,
    defesaAdd int not null,
    requerConstituicao int not null,
    CONSTRAINT item_fk_armadura FOREIGN KEY(idItem) REFERENCES NaoConsumivel(idItem)
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
    CONSTRAINT efeito_porcao CHECK (efeito IN ('1', '2'))
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
    CONSTRAINT tipo_magialivro CHECK (tipo IN ('1', '2', '3'))
);  

CREATE TABLE Clima (
	Id int not null,
    Descricao varchar(50) not null,
    Nome varchar(20) not null,
    Tipo_vantagem char(1) not null,
    Tipo_desvantagem char(1) not null,
    CONSTRAINT clima_pk PRIMARY KEY(Id),
    CONSTRAINT tipo_vantagem_clima CHECK (Tipo_vantagem IN ('1', '2', '3', '4', '5')),
    CONSTRAINT tipo_desvantagem_clima CHECK (Tipo_desvantagem IN ('1', '2', '3', '4', '5'))
); 

CREATE TABLE Regiao (
	Id int not null,
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
	idNPC int not null,
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
	CONSTRAINT vendedor_fk_npc FOREIGN KEY(idNPC) REFERENCES NPC(idNPC)
); 

CREATE TABLE Inimigo (
    idNPC int not null,
    vidaMaxima int not null,
    vidaAtual int not null,
    manaMaxima int not null,
    defesa int not null,
    ataque int not null,
	CONSTRAINT inimigo_fk_npc FOREIGN KEY(idNPC) REFERENCES NPC(idNPC)
); 

CREATE TABLE InstanciaNPC (
	id int not null,
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
    numDialogo int not null,
    status int not null,
    CONSTRAINT interage_pk PRIMARY KEY(numDialogo),
	CONSTRAINT interage_fk_jogador FOREIGN KEY(idJogador) REFERENCES Jogador(id_jogador),
    CONSTRAINT interage_fk_instancianpc FOREIGN KEY(idInstanciaNPC) REFERENCES InstanciaNPC(id)
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
    idMissao int not null,
    nome varchar(20) not null,
    descricao varchar(100) not null,
    recDinheiro int not null,
    recExp int not null,
    idNPC int not null,
    CONSTRAINT missao_pk PRIMARY KEY(idMissao),
	CONSTRAINT missao_fk_npc FOREIGN KEY(idNPC) REFERENCES ProvedorDeMissao(idNPC)
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