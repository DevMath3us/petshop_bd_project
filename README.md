# petshop_bd_project

CREATE DATABASE petshop
CHARACTER SET utf8mb4

COLLATE utf8mb4_unicode_ci;

use petshop;

CREATE TABLE Estoque(
    id_estoque INT AUTO_INCREMENT PRIMARY KEY,
    nome_produto VARCHAR(100) NOT NULL,
    quantidade INT NOT NULL,
    preco DECIMAL(10, 2) NOT NULL,
    data_entrada DATE NOT NULL,
    descricao_produto TEXT
);


CREATE TABLE Clientes(
    id_cliente INT AUTO_INCREMENT PRIMARY KEY,
    nome_cliente VARCHAR(100) NOT NULL,
    telefone VARCHAR(15),
    email VARCHAR(100),
    data_registro DATE NOT NULL,
    endereco VARCHAR(100)
);



create table Funcionarios (
    id_funcionario int auto_increment primary key,
    nome_funcionario varchar(100) not null,
    telefone varchar(15),
    email varchar(100),
    cargo varchar(50),
    salario decimal(10,2),
    data_contratacao date not null
);

create table Servicos (
    id_servico int auto_increment primary key,
    nome_servico varchar(100) not null,
    descricao_servico text,
    preco_servico decimal(10,2) not null,
    duracao_estimada time
);

CREATE TABLE Vendas(
    id_venda INT AUTo_INCREMENT PRIMARY KEY,
    data_venda DATE NOT NULL,
    total DECIMAL(10,2) NOT NULL,
    id_cliente INT NOT NULL,
    id_funcionario INT NOT NULL
);

CREATE TABLE Agendamentos(
    id_agendamento INT AUTO_INCREMENT PRIMARY KEY,
    data_agendamento DATE NOT NULL,
    horario TIME NOT NULL,
    observacoes TEXT
);

CREATE TABLE Itens_Venda(
    id_item_venda INT AUTO_INCREMENT PRIMARY KEY,
    id_venda INT,
    id_estoque INT,
    quantidade_vendida INT NOT NULL,
    preco_unitario DECIMAL(10,2) NOT NULL,
    CONSTRAINT fk_itens_venda_venda FOREIGN KEY (id_venda) REFERENCES Vendas(id_venda),
    CONSTRAINT fk_itens_venda_estoque FOREIGN KEY (id_estoque) REFERENCES Estoque(id_estoque)
);

ALTER TABLE Estoque
ADD INDEX idx_nome_produto (nome_produto);


ALTER TABLE Clientes
ADD INDEX idx_nome_cliente (nome_cliente);
   
ALTER TABLE Funcionarios
ADD INDEX idx_nome_funcionario (nome_funcionario);
   
ALTER TABLE Servicos
ADD INDEX idx_nome_servico (nome_servico);


alter table Vendas
add column id_cliente INT,
    add column id_funcionario INT;
   
alter table Vendas
    ADD INDEX idx_id_cliente (id_cliente),
    ADD INDEX idx_id_funcionario (id_funcionario),
    ADD CONSTRAINT fk_vendas_clientes foreign key (id_cliente) references Clientes(id_cliente),
    ADD CONSTRAINT fk_vendas_funcionario foreign key (id_funcionario) references Funcionarios(id_funcionario);
   
alter table Agendamentos
    ADD COLUMN id_cliente int,
    ADD COLUMN id_servico int,
    ADD COLUMN id_funcionario int,
    ADD INDEX idx_id_cliente_agendamento (id_cliente),
    ADD INDEX idx_id_servico (id_servico),
    ADD INDEX idx_id_funcionario_agendamento (id_funcionario),
    ADD CONSTRAINT fk_agendamento_cliente foreign key (id_cliente) references Clientes (id_cliente),
    ADD CONSTRAINT fk_agendamento_servico foreign key (id_servico) references Servicos (id_servico),
    ADD CONSTRAINT fk_agendamento_funcionario foreign key (id_funcionario) references Funcionarios (id_funcionario);

INSERT INTO Estoque (nome_produto, quantidade, preco, data_entrada, descricao_produto) values
('Ração para Cães','100','50.00','2024-01-10','Ração Premium para cães adultos'),
('Ração para Gatos','80','45.00','24-01-12','Ração Nutritiva para gatos'),
('Brinquedo para Cães','150','25.00','2024-01-15','Brinquedo interativo para cães'),
('Brinquedos para Gatos','120','20.00','2024-01-18','Brinquedo com catnip para gatos'),
('Shampoo para Pets','200','30.00','2024-01-20','Shampoo hipoalergênico para pets'),
('Coleira para Cães','75','15.00','2024-01-22','Coleira ajustável para cães grandes'),
('Coleira para Gatos','50','10.00','2024-01-25','Coleira com guizo para gatos'),
('Ração para filhotes','60','55.00','2024-01-27','Ração especialmente formulada para filhotes'),
('Areia para Gatos','90','35.00','2024-01-30','Areia absorvente para caixa de areia'),
('Vitaminas para Pets','40','75.00','2024-02-02','Suplemento vitamínico para pets'),
('Cama para Cães','35','80.00','2024-02-05','Cama macia para cáes de médio porte'),
('Cama para Gatos','25','65.00','2024-02-07','Cama aconchegante para gatos'),
('Transportadora para Pets','15','120.00','2024-02-10','Caixa de transporte para pets'),
('Escova para Cães','50','22.00','2024-02-12','Escova para manter o pelo do cão limpo'),
('Escova para Gatos','40','18.00','2024-02-15','Escova suave para gatos'),
('Tosa para Cães','20','150.00','2024-02-18','Serviço de tosa para cães'),
('Banho para Cães','30','100.00','2024-02-20','Serviço de banho para Cães'),
('Banho para Gatos','10','810.00','2024-02-22','Serviço de banho para gatos'),
('Vacina para Cães','25','70.00','2024-02-27','Vacina importante para cães'),
('Vacina para Gatps','15','75.00','2024-02-27','Vacina essencial para gatos'),
('Adestramento para Cães','5','300.00','2024-02-28','Curso de adestramento para cães');

INSERT INTO Funcionarios (nome_funcionario, telefone, email, cargo, salario, data_contratacao) VALUES
('Lucas Almeida', '11900000001', 'lucas@gmail.com', 'Atendente', 2000.00, '2024-01-01'),
('Fernanda Costa', '11900000002', 'fernanda@gmail.com', 'Gerente', 3000.00, '2024-01-02'),
('Juliano Silva', '11900000003', 'juliano@gmail.com', 'Veterinário', 4000.00, '2024-01-03'),
('Tatiane Souza', '11900000004', 'tatiane@gmail.com', 'Recepcionista', 1800.00, '2024-01-04'),
('Marcelo Santos', '11900000005', 'marcelo@gmail.com', 'Banho e Tosa', 2200.00, '2024-01-05'),
('Carla Dias', '11900000006', 'carla@gmail.com', 'Adestrador', 2500.00, '2024-01-06'),
('Bruno Ferreira', '11900000007', 'bruno@gmail.com', 'Atendente', 2000.00, '2024-01-07'),
('Patrícia Lima', '11900000008', 'patricia@gmail.com', 'Veterinário', 4000.00, '2024-01-08'),
('André Nascimento', '11900000009', 'andre@gmail.com', 'Recepcionista', 1800.00, '2024-01-09'),
('Cláudia Rocha', '11900000010', 'claudia@gmail.com', 'Gerente', 3000.00, '2024-01-10'),
('Leonardo Almeida', '11900000011', 'leonardo@gmail.com', 'Banho e Tosa', 2200.00, '2024-01-11'),
('Bruna Martins', '11900000012', 'bruna@gmail.com', 'Atendente', 2000.00, '2024-01-12'),
('Gustavo Ribeiro', '11900000013', 'gustavo@gmail.com', 'Adestrador', 2500.00, '2024-01-13'),
('Eduardo Silva', '11900000014', 'eduardo@gmail.com', 'Veterinário', 4000.00, '2024-01-14'),
('Renata Ferreira', '11900000015', 'renata@gmail.com', 'Recepcionista', 1800.00, '2024-01-15');


INSERT INTO Servicos (nome_servico, descricao_servico, preco_servico, duracao_estimada) VALUES
('Banho para Cães Pequenos', 'Banho completo para cães de pequeno porte', 50.00, '00:45:00'),
('Banho para Cães Grandes', 'Banho completo para cães de grande porte', 80.00, '01:15:00'),
('Tosa Completa para Cães', 'Tosa completa com acabamento para cães', 120.00, '01:30:00'),
('Tosa Higiênica', 'Tosa higiênica para áreas específicas', 60.00, '00:30:00'),
('Vacinação', 'Vacinação contra raiva e outras doenças comuns', 70.00, '00:20:00'),
('Consulta Veterinária', 'Consulta com veterinário para check-up geral', 150.00, '01:00:00'),
('Adestramento Básico', 'Sessão de adestramento básico para cães', 200.00, '01:00:00'),
('Hidratação para Cães', 'Tratamento de hidratação para os pelos do cão', 90.00, '00:40:00'),
('Hidratação para Gatos', 'Tratamento de hidratação para os pelos do gato', 85.00, '00:35:00'),
('Banho para Gatos', 'Banho completo para gatos de todos os portes', 70.00, '00:50:00');


INSERT INTO Clientes (nome_cliente, telefone, email, endereco, data_registro) VALUES
('Carlos Silva', '11987654321', 'carlos@gmail.com', 'Rua A, 123', '2024-01-01'),
('Maria Oliveira', '11976543210', 'maria@gmail.com', 'Rua B, 234', '2024-01-02'),
('José Santos', '11965432109', 'jose@gmail.com', 'Rua C, 345', '2024-01-03'),
('Ana Pereira', '11954321898', 'ana@gmail.com', 'Rua D, 456', '2024-01-04'),
('Roberto Lima', '11943210987', 'roberto@gmail.com', 'Rua E, 567', '2024-01-05'),
('Patrícia Costa', '11932109876', 'patricia@gmail.com', 'Rua F, 678', '2024-01-06'),
('Fernando Almeida', '11921098765', 'fernando@gmail.com', 'Rua 6, 789', '2024-01-07'),
('Juliana Martins', '11910987654', 'juliana@gmail.com', 'Rua H, 890', '2024-01-08'),
('Renato Sousa', '11909876543', 'renato@gmail.com', 'Rua I, 901', '2024-01-09'),
('Roberta Ferreira', '11998765432', 'roberta@gmail.com', 'Rua J, 012', '2024-01-10'),
('Fernanda Ribeiro', '11987654321', 'fernanda@gmail.com', 'Rua K, 123', '2024-01-11'),
('Marcos Rocha', '11976543210', 'marcos@gmail.com', 'Rua L, 234', '2024-01-12'),
('Tatiane Almeida', '11965432109', 'tatiane@gmail.com', 'Rua M, 345', '2024-01-13'),
('Gustavo Mendes', '11954321098', 'gustavo@gmail.com', 'Rua N, 456', '2024-01-14'),
('Aline Santos', '11943210987', 'aline@gmail.com', 'Rua 0, 567', '2024-01-15'),
('Ricardo Nascimento', '11932109876', 'ricardo@gmail.com', 'Rua P, 678', '2024-01-16'),
('Daniela Lima', '11921898765', 'daniela@gmail.com', 'Rua Q, 789', '2024-01-17'),
('Leonardo Silva', '11910987654', 'leonardo@gmail.com', 'Rua R, 890', '2024-01-18'),
('Sofia Costa', '11909876543', 'sofia@gmail.com', 'Rua S, 901', '2024-01-19'),
('André Martins', '11998765432', 'andre@gmail.com', 'Rua T, 012', '2024-01-20');
   
INSERT INTO Vendas (data_venda, total, id_cliente, id_funcionario) VALUES
(2024-03-25, 200.00, 6, 6);

select * from itens_venda;
