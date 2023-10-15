# Base-de-Dados-Empresa-VIEW-
CREATE TABLE Produtos (
    ProdutoID INT PRIMARY KEY,
    Nome VARCHAR(255),
    Marca VARCHAR(255),
    Fornecedor VARCHAR(255),
    Estoque INT,
    EstoqueMinimo INT,
    Preco DECIMAL(10, 2),
    DataValidade DATE
);

-- Inserir dados com a data de validade
INSERT INTO Produtos (ProdutoID, Nome, Marca, Fornecedor, Estoque, EstoqueMinimo, Preco, DataValidade)
VALUES (1, 'Lapis', 'BIC', 'BIC', 50, 10, 1.99, '2028-10-31'),
       (2, 'Banana', 'Turma da Monica', 'Tauste', 30, 5, 7.99, '2023-11-15'),
       (3, 'miojo', 'Turma da Monica', 'Nissin', 30, 5, 7.99, '2024-06-15'),
       (4, 'Bolo', 'Puma', 'Balduco', 30, 5, 7.99, '2023-04-27'),
       (5, 'Arroz', 'Dona Benta', 'Roldão', 20, 15, 5.99, '2023-09-30');
       
       CREATE VIEW ProdutosComMarcas AS
SELECT ProdutoID, Nome AS Produto, Marca
FROM Produtos;

CREATE VIEW ProdutosComFornecedores AS
SELECT ProdutoID, Nome AS Produto, Fornecedor
FROM Produtos;

CREATE VIEW ProdutosComFornecedoresEMarcas AS
SELECT ProdutoID, Nome AS Produto, Marca, Fornecedor
FROM Produtos;

CREATE VIEW ProdutosComEstoqueBaixo AS
SELECT ProdutoID, Nome AS Produto, Estoque, EstoqueMinimo
FROM Produtos
WHERE Estoque < EstoqueMinimo;

CREATE VIEW ProdutosComValidadeVencida AS
SELECT ProdutoID, Nome AS Produto, Marca, DataValidade
FROM Produtos
WHERE DataValidade < CURDATE();

SELECT ProdutoID, Nome AS Produto, Preco
FROM Produtos
WHERE Preco > (SELECT AVG(Preco) FROM Produtos);
