
# Cabelos incríveis
# Estudo de Caso: Salão de Cabeleireiro "Cabelos Incríveis"

### Cabelos Incríveis 

## Contexto:
O salão de cabeleireiro "Cabelos Incríveis" é um estabelecimento localizado em uma área movimentada da cidade. O salão oferece uma variedade de serviços, incluindo cortes de cabelo, coloração, tratamentos capilares, manicure e pedicure. Eles têm uma equipe de cabeleireiros talentosos e uma base de clientes fiéis.
### Desafio:
O salão de cabeleireiro "Cabelos Incríveis" está enfrentando dificuldades para gerenciar eficientemente seus clientes, agendamentos, estoque de produtos e informações dos funcionários. Eles precisam de um sistema de banco de dados para ajudar a organizar e automatizar esses processos. 
### Requisitos do Sistema:
• Gerenciamento de Clientes: Cadastro de novos clientes com informações como nome, endereço, telefone, e-mail, preferências de serviços, histórico de serviços realizados, etc. 
O registro de serviços realizados por cada cliente, incluindo datas, tipos de serviço, cabeleireiro responsável, etc.
O Possibilidade de atualização e exclusão de informações de clientes. 
### Agendamento de Serviços:
Capacidade de agendar serviços para clientes, incluindo data, horário, tipo de serviço, cabeleireiro responsável, etc. o Visualização rápida de disponibilidade de horários e cabeleireiros para agendamentos.   
### Gerenciamento de Estoque:
Controle de estoque de produtos utilizados no salão, como tinturas, shampoos, condicionadores, etc.
Registro de entrada e saída de produtos, incluindo quantidades e datas. 
### Informações dos Funcionários: 
Cadastro de informações dos funcionários, incluindo nome, função, horário de trabalho, salário, etc.
Atribuição de serviços realizados por cada funcionário e acompanhamento de seu desempenho.

# Modelo Lógico do Banco de Dados:
Modelação do banco de dados baseado nos requisidos exigidos acima, definindo um modelo lógico básico para o banco de dados do salão de cabeleireiro "Cabelos Incríveis".

# Especificação de elementos do banco de dados.

• Tabelas:
Clientes ▪ Cliente_ID (Chave Primária) ▪ Nome ▪ Endereço ▪ Telefone ▪ E-mail ▪ Preferências o Serviços ▪ Serviço_ID (Chave Primária) ▪ Tipo ▪ Descrição ▪ Preço o Agendamentos ▪ Agendamento_ID (Chave Primária) ▪ Cliente_ID (Chave Estrangeira referenciando a tabela Clientes) ▪ Serviço_ID (Chave Estrangeira referenciando a tabela Serviços) ▪ Data ▪ Horário ▪ Cabeleireiro o Estoque ▪ Produto_ID (Chave Primária) ▪ Nome ▪ Quantidade ▪ Data_Entrada ▪ Data_Saída o Funcionários ▪ Funcionário_ID (Chave Primária) ▪ Nome ▪ Função ▪ Horário_Trabalho ▪ Salário

# Modelo Lógico com as normalizações

![normalizacaolivre png](https://github.com/user-attachments/assets/a06aca03-546f-434e-bdf4-29df2feb6169)

## 1 Normalização

![primeiranormalizacao](https://github.com/user-attachments/assets/998eeba5-0112-4379-98f3-b0ea0100e584)

## 2 Normalização
![segundanormalizacao](https://github.com/user-attachments/assets/b7c7e60e-2967-4657-9fab-03e5aa24a6e9)

## 3 Normalização




# Modelo Físico
### Código escrito em sql
```sql create database cabelosincriveisdb; use cabelosincriveis;
create database cabelosincriveis;
use cabelosincriveis

create table endereco (
idendereco INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
tipologradouro VARCHAR(20) NOT NULL DEFAULT 'not null',
logradouro VARCHAR(50) NOT NULL DEFAULT 'not null',
numero VARCHAR(10) NOT NULL DEFAULT 'not null',
complemento VARCHAR(20) NOT NULL,
cep VARCHAR(9) NOT NULL DEFAULT 'not null',
bairro VARCHAR(40) NOT NULL DEFAULT 'not null',
cidade VARCHAR(50) NOT NULL DEFAULT 'not null',
uf CHAR(2) NOT NULL DEFAULT 'not null',
pais VARCHAR(30) NOT NULL DEFAULT '"Brasil"');

create table contato (
idcontato INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
comercial VARCHAR(15) NOT NULL,
residencial VARCHAR(15) NOT NULL,
celular VARCHAR(15) NOT NULL DEFAULT 'not null',
email VARCHAR(50) NOT NULL,
redesocial VARCHAR(30) NOT NULL);

create table servico (
idservico INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
servicos ENUM ("corte","lavagem","hidratacao","coloracao","alisamento","alongamento","luzes","mechas","manicure","pedicure") NOT NULL DEFAULT not null,
preco DECIMAL(6,2) NOT NULL DEFAULT not null);

create table servico ( produto (
idproduto INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
nome_produto VARCHAR(40) NOT NULL DEFAULT 'not null',
descricao TEXT NOT NULL DEFAULT 'not null',
marca VARCHAR(15) NOT NULL DEFAULT 'not null',
preco DECIMAL(6,2) NOT NULL DEFAULT not null,
tipo VARCHAR(15) NOT NULL DEFAULT 'not null',
cor VARCHAR(20) NOT NULL DEFAULT 'not null',
fabricacao DATE NOT NULL DEFAULT not null,
validade DATE NOT NULL DEFAULT not null);

create table  funcionario (
idfuncionario INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
idcontato INT NOT NULL,
idendereco INT NOT NULL,
nome_funcionario VARCHAR(50) NOT NULL DEFAULT 'not null',
funcao VARCHAR(40) NOT NULL DEFAULT 'not null',
turno ENUM ("Manhã","Tarde","Noite","Integral") NOT NULL DEFAULT not null,
matricula VARCHAR(10) NOT NULL UNIQUE DEFAULT 'not null',
salario DECIMAL(7,2) NOT NULL DEFAULT not null,
comissao DECIMAL(7,2),
nomesocial VARCHAR(50),
cpf VARCHAR(14) NOT NULL UNIQUE DEFAULT 'not null',
genero VARCHAR(20) NOT NULL,
pcd BOOLEAN(1) NOT NULL DEFAULT not null);

create table cliente (
idcliente INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
idendereco INT NOT NULL,
idcontato INT NOT NULL,
nome_cliente VARCHAR(50) NOT NULL DEFAULT 'not null',
cpf VARCHAR(14) NOT NULL UNIQUE,
data_nascimento DATE NOT NULL DEFAULT not null,
nomesocial VARCHAR(50),
genero VARCHAR(20));

create table agendamento (
idagendamento INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
idservico INT NOT NULL,
idfuncionario INT NOT NULL,
idcliente INT NOT NULL,
data_agendamento DATE NOT NULL DEFAULT not null,
hora_agendamento TIME NOT NULL DEFAULT not null);

create table estoque (
idestoque INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
idproduto INT NOT NULL,
quantidade INT(3) NOT NULL DEFAULT not null);

create table venda (
idvenda INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
idcliente INT NOT NULL,
idfuncionario INT NOT NULL,
idservico INT NOT NULL,
data_hora DATETIME NOT NULL DEFAULT current_timestamp(),
desconto DECIMAL(5,2) DEFAULT default 0,
total_venda DECIMAL(7,2) NOT NULL DEFAULT not null);

create table (
idpagamento INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
idvenda INT NOT NULL,
forma_pagamento ENUM ("Dinheiro","Débito","Pix","Crédito") NOT NULL DEFAULT not null,
valor_pagamento DECIMAL(7,2) NOT NULL DEFAULT not null,
parcelamento INT(2) NOT NULL DEFAULT 1);

create table detalhe_venda (
iddetalhe_venda INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
idvenda INT NOT NULL,
idproduto INT NOT NULL,
idfuncionario INT NOT NULL,
idservico INT NOT NULL,
preco DECIMAL(7,2) NOT NULL,
quantidade INT(3) NOT NULL DEFAULT 1);

```

## Modelo de Entidade Relacional

#### Diagrama do relacionamento Casa Oliveira

![modelorelacional cabelosincriveis](https://github.com/user-attachments/assets/f0ee11ec-7cde-4344-97ac-a563ac54997e)
