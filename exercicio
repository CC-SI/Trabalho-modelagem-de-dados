---------- Cadastro de Formatura ----------

CREATE TABLE Curso (
    id INT PRIMARY KEY NOT NULL,
    nome VARCHAR(30) NOT NULL
);

CREATE TABLE Faculdade (
    id INT PRIMARY KEY NOT NULL,
    nome VARCHAR(50) NOT NULL
);

CREATE TABLE Representante (
    id INT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    telefone CHAR(15) UNIQUE NOT NULL
);

CREATE TABLE Forma_Pagamento (
    id INT PRIMARY KEY,
    tipo VARCHAR(20) NOT NULL
);

CREATE TABLE Formatura (
    id INT PRIMARY KEY NOT NULL,
    id_curso INT NOT NULL,
    id_faculdade INT NOT NULL,
    id_representante INT NOT NULL,
    id_forma_pagamento INT NOT NULL,
    valor_pagamento FLOAT NOT NULL,
    FOREIGN KEY (id_curso) REFERENCES Curso(id),
    FOREIGN KEY (id_faculdade) REFERENCES Faculdade(id),
    FOREIGN KEY (id_representante) REFERENCES Representante(id),
    FOREIGN KEY (id_forma_pagamento) REFERENCES Forma_Pagamento(id)
);

---------- Cadastro de Evento ----------

CREATE TABLE Evento (
    id INT PRIMARY KEY NOT NULL,
    nome VARCHAR(30) NOT NULL,
    descricao VARCHAR(250) NOT NULL,
    duracao INT NOT NULL
);

CREATE TABLE Status_Evento (
    id INT PRIMARY KEY NOT NULL,
    status VARCHAR(10) NOT NULL
);

CREATE TABLE Endereco (
    id INT PRIMARY KEY NOT NULL,
    rua VARCHAR(50) NOT NULL,
    bairro VARCHAR(50) NOT NULL,
    cep CHAR(9) UNIQUE NOT NULL,
    cidade VARCHAR(30) NOT NULL,
    estado CHAR(2) NOT NULL
);

CREATE TABLE Evento_Formatura (
    id_formatura INT NOT NULL,
    id_evento INT NOT NULL,
    id_endereco INT NOT NULL,
    data DATE NOT NULL,
    id_status_evento INT NOT NULL,
    nova_data DATE,
    evento_fechado CHAR(1) NOT NULL CHECK (evento_fechado IN ('S', 'N')),
    convidados INT,
    PRIMARY KEY (id_formatura, id_evento),
    FOREIGN KEY (id_formatura) REFERENCES Formatura(id),
    FOREIGN KEY (id_evento) REFERENCES Evento(id),
    FOREIGN KEY (id_endereco) REFERENCES Endereco(id),
    FOREIGN KEY (id_status_evento) REFERENCES Status_Evento(id),
    CHECK ((id_status_evento = 1 AND nova_data IS NULL) OR (id_status_evento = 2 AND nova_data IS NULL) 
    	OR (id_status_evento = 3 AND nova_data IS NOT NULL)),
    CHECK ((evento_fechado = 'S' AND convidados IS NOT NULL) OR (evento_fechado = 'N' AND convidados IS NULL))
);

---------- Cadastro de Funcionário ----------

CREATE TABLE Uniforme (
    id INT PRIMARY KEY NOT NULL,
    descricao VARCHAR(100) NOT NULL
);

CREATE TABLE Profissao (
    id INT PRIMARY KEY NOT NULL,
    nome VARCHAR(50) NOT NULL,
    limite_hora_extra INT NOT NULL,
    valor_hora_extra FLOAT NOT NULL,
    uniformizado CHAR(1) NOT NULL CHECK (uniformizado IN ('S', 'N')),
    id_uniforme INT,
    FOREIGN KEY (id_uniforme) REFERENCES Uniforme(id),
    CHECK ((uniformizado = 'S' AND id_uniforme IS NOT NULL) OR (uniformizado = 'N' AND id_uniforme IS NULL))
);

CREATE TABLE Status_Funcionario (
    id INT PRIMARY KEY NOT NULL,
    status VARCHAR(10) NOT NULL
);

CREATE TABLE Funcionario (
    matricula INT PRIMARY KEY,
    nome VARCHAR(50),
    telefone CHAR(15) UNIQUE,
    id_profissao INT,
    salario FLOAT,
    id_status_funcionario INT NOT NULL,
    FOREIGN KEY (id_profissao) REFERENCES Profissao(id),
    FOREIGN KEY (id_status_funcionario) REFERENCES Funcionario(id),
    CHECK ((id_status_funcionario = 1 AND matricula, nome, telefone, id_profissao, salario IS NOT NULL) 
    	OR (id_status_funcionario = 2 AND matricula, nome, telefone, id_profissao, salario IS NULL))
);

CREATE TABLE Funcionario_Evento (
    id_evento INT NOT NULL,
    id_funcionario INT NOT NULL,
    horas INT NOT NULL,
    PRIMARY KEY (id_evento, id_funcionario),
    FOREIGN KEY (id_evento) REFERENCES Evento(id),
    FOREIGN KEY (id_funcionario) REFERENCES Funcionario(id)
);

---------- Cadastro de Buffet ----------

CREATE TABLE Buffet (
    cpnj INT PRIMARY KEY NOT NULL,
    nome VARCHAR(50) NOT NULL,
    id_endereco INT UNIQUE NOT NULL,
    inicio_parceria DATE NOT NULL,
    termino_parceria DATE NOT NULL,
    FOREIGN KEY (id_endereco) REFERENCES Endereco(id)
);

CREATE TABLE Cardapio (
    id INT PRIMARY KEY NOT NULL,
    id_buffet INT NOT NULL,
    descricao VARCHAR(250) NOT NULL,
    preco_por_pessoa FLOAT NOT NULL,
    FOREIGN KEY (id_buffet) REFERENCES Buffet(id)
);
