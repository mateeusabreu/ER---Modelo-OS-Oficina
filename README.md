# ER--Modelo-OS-Oficina

-- CLIENTE
CREATE TABLE Cliente (
    idCliente INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100),
    telefone VARCHAR(20),
    cpf_cnpj VARCHAR(32),
    endereco VARCHAR(100)
);

-- VEÍCULO
CREATE TABLE Veiculo (
    idVeiculo INT PRIMARY KEY AUTO_INCREMENT,
    idCliente INT,
    placa VARCHAR(10),
    marca VARCHAR(48),
    modelo VARCHAR(50),
    ano VARCHAR(10),
    cor VARCHAR(29),
    tipo_combustivel VARCHAR(20),
    FOREIGN KEY (idCliente) REFERENCES Cliente(idCliente)
);

-- EQUIPE DE MECÂNICOS
CREATE TABLE EquipeMecanicos (
    idEquipe INT PRIMARY KEY AUTO_INCREMENT,
    nome_equipe VARCHAR(50)
);

-- MECÂNICO
CREATE TABLE Mecanico (
    idMecanico INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100),
    endereco VARCHAR(130),
    especialidade VARCHAR(50)
);

-- RELAÇÃO N:N MECÂNICO x EQUIPE
CREATE TABLE MecanicoEquipe (
    idEquipe INT,
    idMecanico INT,
    PRIMARY KEY (idEquipe, idMecanico),
    FOREIGN KEY (idEquipe) REFERENCES EquipeMecanicos(idEquipe),
    FOREIGN KEY (idMecanico) REFERENCES Mecanico(idMecanico)
);

-- PEÇAS
CREATE TABLE Peca (
    idPeca INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100),
    descricao TEXT,
    valor_unitario DECIMAL(10,2),
    estoque_atual INT
);

-- SERVIÇOS DE REFERÊNCIA
CREATE TABLE ServicoReferencia (
    idServicoRef INT PRIMARY KEY AUTO_INCREMENT,
    descricao TEXT,
    valor_base DECIMAL(10,2)
);

-- ORDEM DE SERVIÇO
CREATE TABLE OrdemServico (
    idOrdemServico INT PRIMARY KEY AUTO_INCREMENT,
    idVeiculo INT,
    idEquipe INT,
    data_emissao DATE,
    data_entrega_prevista DATE,
    status VARCHAR(50),
    valor_total DECIMAL(10,2),
    autorizado_cliente BOOLEAN,
    FOREIGN KEY (idVeiculo) REFERENCES Veiculo(idVeiculo),
    FOREIGN KEY (idEquipe) REFERENCES EquipeMecanicos(idEquipe)
);

-- SERVIÇOS EXECUTADOS
CREATE TABLE ServicoExecutado (
    idServicoExecutado INT PRIMARY KEY AUTO_INCREMENT,
    idOrdemServico INT,
    idServicoRef INT,
    descricao TEXT,
    valor_final DECIMAL(10,2),
    FOREIGN KEY (idOrdemServico) REFERENCES OrdemServico(idOrdemServico),
    FOREIGN KEY (idServicoRef) REFERENCES ServicoReferencia(idServicoRef)
);

-- PEÇAS USADAS EM OS
CREATE TABLE PecaUsada (
    idPecaUsada INT PRIMARY KEY AUTO_INCREMENT,
    idOrdemServico INT,
    idPeca INT,
    quantidade INT,
    valor_total DECIMAL(10,2),
    FOREIGN KEY (idOrdemServico) REFERENCES OrdemServico(idOrdemServico),
    FOREIGN KEY (idPeca) REFERENCES Peca(idPeca)
);
