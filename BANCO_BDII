create database db_shopping;
use db_shopping;

CREATE TABLE cliente(
	CPF VARCHAR(15) not null,
	NOME VARCHAR(30) NOT NULL, 
    EMAIL VARCHAR(20) NOT NULL,
    SEXO VARCHAR(10) NOT NULL,
    ENDERECO VARCHAR(50) NOT NULL,
    CONSTRAINT PK_CPF PRIMARY KEY(CPF)    
);

CREATE TABLE Loja_Roupa(
	CNPJ_LOJA VARCHAR(20) PRIMARY KEY, 
    NOME VARCHAR(20) NOT NULL, 
    RAZAO_SOCIAL VARCHAR(30) NOT NULL
 );

CREATE TABLE Roupa
(	
	ID varchar(3) PRIMARY KEY,
	Descricao VARCHAR(50),
    Estoque INT NOT NULL DEFAULT 0
);

CREATE TABLE RoupaVenda(
	Venda INT,
    Roupas VARCHAR(3), 
    Quantid int,
    Constraint fk_Roupavenda Foreign Key(Roupas) references Roupa(ID)
);

CREATE TABLE Restaurante(
	CNPJ_RESTAURANTE VARCHAR(20) PRIMARY KEY, 
    NOME VARCHAR(20) NOT NULL, 
    RAZAO_SOCIAL VARCHAR(30) NOT NULL
);

CREATE TABLE Cardapio
(	
	ID_Cardapio varchar(10) PRIMARY KEY,
	Descricao VARCHAR(50),
    Estoque INT NOT NULL DEFAULT 0
);

CREATE TABLE Cardapio_Item(
	Venda INT,
    Itens VARCHAR(10), 
    Quantid int,
    Constraint fk_CardapioVenda Foreign Key(Itens) references Cardapio(ID_Cardapio)
);

#Prcedure que retorna a quantidade de item que quero no cardápio(limita)
DELIMITER $$
CREATE PROCEDURE Selecionar_Produtos(IN quantidade INT)
BEGIN
SELECT * FROM Cardapio_Item
LIMIT quantidade;
END $$
DELIMITER ;

#Trigger que atualiza a quantidade de roupas do estoque depois do insert
DELIMITER $

CREATE Trigger Tgr_Roupa_Insert
AFTER INSERT
ON RoupaVenda
FOR EACH ROW
BEGIN
	UPDATE Roupa SET ESTOQUE = ESTOQUE - NEW.Quantid
WHERE ID = NEW.Roupas;
END $

DELIMITER ;

# Criação da View para vizualização de dados do cliente
CREATE OR REPLACE VIEW Vizualiza AS SELECT * FROM CLIENTE;
CREATE OR REPLACE VIEW Vizualiza1 AS SELECT * FROM Loja_Roupa;

#Função que verifica se tal cliente tem cadastro
CREATE FUNCTION FN_CLIENTE(numero Varchar(15))
RETURNS VARCHAR(60) DETERMINISTIC 
RETURN (SELECT CONCAT('CPF: ', C.CPF, ' - ', 'NOME: ', C.NOME) from cliente C where numero = C.CPF);





