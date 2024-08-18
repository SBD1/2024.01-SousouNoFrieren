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
    idItem int not null,
    quantidade int not null,
    idInstancia_Item int not null,
    CONSTRAINT guarda_fk_inv FOREIGN KEY(idInventario) REFERENCES Inventario(id_inventario),
    CONSTRAINT guarda_fk_item FOREIGN KEY(idItem) REFERENCES Item(idItem),
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
    CONSTRAINT item_fk_magialivro FOREIGN KEY(idItem) REFERENCES Consumivel(idItem),
    CONSTRAINT tipo_magialivro CHECK (tipo IN ('1', '2', '3'))
); 

```