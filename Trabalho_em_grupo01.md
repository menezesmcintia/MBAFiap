# Trabalho em Grupo 01

Nome: Cintia Maria de Souza Menezes RM: 353700

# Parte 1:

✓ Crie 3 tabelas para um site de venda de sapatos;
✓ Adicionar campos, se desejar;
✓ Alguns campos são conceituais, exercitem a modelagem;
✓ Entrega: Os scripts de criação das tabelas para MySQL, Cassandra e MongoDB;

# **MySQL**

---

# Preparando o Docker

## Passo 1: Configurando o Docker

Se você ainda não tem um container do MySQL, vamos criar um. Use o comando abaixo para rodar um container do MySQL utilizando a imagem oficial:

```bash
docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=sua_senha -d mysql:latest

```

Neste comando:

- `-name mysql-container` atribui um nome ao seu container.
- `e MYSQL_ROOT_PASSWORD=sua_senha` define a senha do usuário root do MySQL (substitua `sua_senha` por uma senha de sua escolha).
- `d mysql:latest` especifica que queremos rodar a imagem mais recente do MySQL em modo detached (em segundo plano).

## Passo 2: Acessando o MySQL

Após o container estar em execução, você pode acessar o MySQL com o seguinte comando:

```bash
docker exec -it mysql-container mysql -uroot -p

```

Você será solicitado a inserir a senha definida anteriormente.

## Passo 3: Criando a Tabela

Dentro do MySQL, crie a base de dados e a tabela de clientes. Execute os seguintes comandos no prompt do MySQL:

```sql
CREATE DATABASE site_sapatos;
USE site_sapatos;

CREATE TABLE Clientes (
    CPF VARCHAR(11) PRIMARY KEY,
    Nome VARCHAR(100),
    Endereco VARCHAR(255),
    CEP VARCHAR(8),
    Email VARCHAR(100),
    Telefones VARCHAR(20)
);

```

Esses comandos criarão uma nova base de dados chamada `site_sapatos` e, dentro dela, a tabela `clientes` conforme discutido.

## Passo 4: Verificação

Para verificar se a tabela foi criada corretamente, use o comando:

```sql
SHOW TABLES;

```

E para ver a estrutura da tabela:

```sql
DESCRIBE clientes;

```

Siga estes passos e avise-me se tudo funcionou como esperado ou se precisar de ajuda em algum dos passos!

# Verificando Imagens Existentes no Docker

Se você já possui uma imagem do MySQL, não é necessário criar outra. Veja como verificar se já possui um container do MySQL rodando ou imagens do MySQL disponíveis no Docker.

## Passo 1: Listar Containers

Para ver todos os containers (ativos e inativos), use o comando:

```bash
docker ps -a

```

Este comando mostra todos os containers. Se houver um container do MySQL já configurado, ele aparecerá na lista.

## Passo 2: Listar Imagens

Para ver as imagens disponíveis no Docker, use o comando:

```bash
docker images

```

Este comando listará todas as imagens armazenadas localmente, incluindo as do MySQL, se houver.

## Passo 3: Acessar um Container Existente

Se encontrar um container do MySQL que deseja usar e ele estiver inativo, inicie o container com o comando:

```bash
docker start nome_do_container

```

Para acessar o MySQL dentro de um container ativo, use:

```bash
docker exec -it nome_do_container mysql -uroot -p

```

Você será solicitado a inserir a senha do usuário root do MySQL.

## Passo 4: Acessar a Base de Dados

Se já tiver uma base de dados criada, você pode acessá-la diretamente.

---

# Scripts para criação do Banco MySQL

```sql
CREATE DATABASE Sapatos;
USE Sapatos;
```

**Tabela de Clientes:**

```sql
CREATE TABLE Clientes (
    CPF VARCHAR(11) PRIMARY KEY,
    Nome VARCHAR(100),
    Endereco VARCHAR(255),
    CEP VARCHAR(8),
    Email VARCHAR(100),
    Telefones VARCHAR(20)
);
```

Tabela de Produtos:

```sql
CREATE TABLE Produtos (
    Codigo VARCHAR (10) INT PRIMARY KEY,
    Nome VARCHAR(100),
    Modelo VARCHAR(50),
    Fabricante VARCHAR(100),
    Cor VARCHAR(50),
    Tam VARCHAR(10)
);
```

Tabela de Pedidos:

```sql
CREATE TABLE Pedidos(
    PedidoID INT PRIMARY KEY AUTO_INCREMENT,
    ClienteCPF VARCHAR(11),
    Endereco VARCHAR(255),
    CEP VARCHAR(8),
    Itens VARCHAR (300),
    Qtdes VARCHAR (100),
    ValorPago DECIMAL(10, 2),
    FOREIGN KEY (ClienteCPF) REFERENCES Clientes(CPF)
);
```

Inserindo dados na tabela de Cliente:

```sql
INSERT INTO Clientes (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES
('24204365409', 'Tiago Cruz', 'Rua do Oratorio, 520', '14520000', 'tiago.cde@email.com', '19985653625'),
('73418177320', 'Zilda Gonzalez', 'Avenida Central, 1200', '35065320', 'zildadbl@email.com', '21958568240'),
('74663094097', 'Eduardo Silva', 'Rua estrela da manha, 65', '45262360', 'eduardosil@email.com', '11985634154'),
('45678901234', 'Diego Feitosa', 'Praca da arvore, 32', '52657025', 'digdigae@email.com', '48956802054'),
('56789012345', 'Andre Luiz', 'Rua da esperança, 202', '58742-000', 'andrezito52@email.com', '11985648000'),
('67890123456', 'Julia Mendonça', 'Estrada do pinheiro, 15300', '81526000', 'juliamm@email.com', '11985268432'),
('78901234567', 'Carlos Rego', 'Rua Lucio dos gato, 666', '78901234', 'miaumiau@email.com', '11930307070'),
('89012345678', 'Eloy Casapequena', 'Estrada do no corredio, 999', '89012345', 'eloyzinho@email.com', '11965413252'),
('90123456789', 'Gabriel Soares', 'Rua do piper, 34', '9012000', 'gabshappy@email.com', '52956802154'),
('01234567890', 'Elizabeth darcy', 'Avenida Jane Austen, 1820', '32529633', 'elizalovedarcy@email.com', '52985653214');
```

Inserindo dados na tabela de Produto:

```sql
INSERT INTO Produtos (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES
('SKU00050', 'Sapato Social', 'Classico', 'Sapatos SA', 'Preto', '40'),
('SKU00051', 'Sapato Esportivo', 'Runner', 'Esportivos Ltda', 'Branco', '42'),
('SKU00052', 'Sandália Casual', 'Verão', 'Moda Praia', 'Azul', '38'),
('SKU00053', 'Bota Trekking', 'Aventura', 'Outdoor Gear', 'Marrom', '41'),
('SKU00054', 'Mocassim', 'Confort', 'Elegance Shoes', 'Bege', '39'),
('SKU00055', 'Chinelo', 'Simples', 'Conforto SA', 'Verde', '37'),
('SKU00056', 'Sapatênis', 'Casual', 'Urbano', 'Cinza', '40'),
('SKU00057', 'Tênis Corrida', 'FastRun', 'Speed Shoes', 'Vermelho', '42'),
('SKU00058', 'Sapato Casual', 'Dia a Dia', 'Praticidade', 'Preto', '39'),
('SKU00059', 'Sandália Esportiva', 'Sporty', 'Adventure', 'Preto', '40');
```

Inserindo dados em Pedidos:

```sql
INSERT INTO Pedidos (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES
('24204365409', 'Rua do Oratorio, 520', '14520000', '12345678', 'Sapato Social', '1', 299.90),
('73418177320', 'Avenida Central, 1200', '35065320', 'Sapato Esportivo', '2', 699.99),
('74663094097', 'Eduardo Silva', 'Rua estrela da manha, 65', 'Sandália Casual', '1', 59.99),
('45678901234', 'Diego Feitosa', 'Praca da arvore, 32', 'Bota Trekking', '1', 890.00),
('56789012345', 'Andre Luiz', 'Rua da esperança, 202', '58742-000', 'Mocassim', '2', 349.00),
('67890123456', 'Julia Mendonça', 'Estrada do pinheiro, 15300', '81526000', 'Chinelo', '3', 39.90),
('78901234567', 'Carlos Rego', 'Rua Lucio dos gato, 666', '78901234', 'Sapatênis', '1', 279.90),
('89012345678', 'Eloy Casapequena', 'Estrada do no corredio, 999', '89012345', 'Tênis Corrida', '1', 399.90),
('90123456789', 'Gabriel Soares', 'Rua do piper, 34', '9012000', 'Sapato Casual', '2', 559.80),
('01234567890', 'Elizabeth darcy', 'Avenida Jane Austen, 1820', '32529633', 'Sandália Esportiva', '1', 249.90);
```

---

# Cassandra

---

# Instalando o Cassandra no Docker

Vamos configurar o Cassandra no Docker. Siga o passo a passo abaixo para configurar e executar um container do Cassandra usando o Docker:

## Passo 1: Puxar a Imagem do Cassandra

Primeiro, puxe a imagem oficial do Cassandra do Docker Hub. Abra um terminal e execute o seguinte comando para obter a imagem mais recente do Cassandra:

```bash
docker pull cassandra:latest

```

## Passo 2: Criar e Executar um Container do Cassandra

Após puxar a imagem, crie e execute um container do Cassandra com o comando abaixo:

```bash
docker run --name cassandra-container -p 9042:9042 -d cassandra:latest

```

Neste comando:

- `-name cassandra-container` atribui um nome ao container.
- `p 9042:9042` mapeia a porta 9042 do container para a porta 9042 do host, que é a porta padrão usada pelo Cassandra.
- `d cassandra:latest` especifica que queremos usar a imagem mais recente do Cassandra em modo detached (em segundo plano).

## Passo 3: Verificar se o Container Está Rodando

Para verificar se o container do Cassandra está rodando corretamente, use o comando:

```bash
docker ps

```

Esse comando lista todos os containers ativos. O `cassandra-container` deve aparecer na lista.

## Passo 4: Acessar o Cassandra

Para interagir com o Cassandra dentro do container, utilize o `cqlsh`, um shell interativo para trabalhar com o Cassandra. Execute o seguinte comando para acessar o shell do Cassandra:

```bash
docker exec -it cassandra-container cqlsh

```

Agora você está no shell do Cassandra e pode começar a criar seu banco de dados e tabelas.

Estes são os passos iniciais para configurar e começar a usar o Cassandra no Docker. 

---

---

# Comandos Úteis de Cassandra

## 1. Criar uma Keyspace

Para criar um keyspace no Cassandra, você pode usar o comando `CREATE KEYSPACE` no CQLSH.

## 2. Criar uma Tabela

Para criar uma tabela dentro de um keyspace no Cassandra, utilize o comando `CREATE TABLE`.

## 3. Listar Tabelas de um Keyspace Específico

Para listar as tabelas em um keyspace específico usando o CQLSH do Cassandra, siga os passos abaixo:

### Passo 1: Acessar o CQLSH

Primeiro, abra o shell do Cassandra digitando `cqlsh` no terminal.

### Passo 2: Listar as Tabelas de um Keyspace Específico

Para ver todas as tabelas dentro de um keyspace específico, use o comando `DESCRIBE KEYSPACE nome_do_keyspace`. Por exemplo, para ver todas as tabelas no keyspace `Sapatos`, você usaria:

```sql
DESCRIBE KEYSPACE Sapatos;

```

Este comando mostrará não apenas as tabelas, mas também outras entidades como tipos definidos pelo usuário, índices, funções e agregações associadas ao keyspace especificado.

## 4. Deletar uma Tabela do Keyspace

Para deletar uma tabela no Cassandra usando a interface de linha de comando (CQLSH), siga os passos abaixo:

### Passo 1: Acessar o CQLSH

Primeiro, abra o shell do Cassandra digitando `cqlsh` no terminal.

### Passo 2: Deletar a Tabela

Uma vez dentro do CQLSH, você pode deletar uma tabela com o seguinte comando:

```sql
DROP TABLE IF EXISTS nome_do_keyspace.nome_da_tabela;

```

Por exemplo, para deletar a tabela `Clientes` no keyspace `Sapatos`, você usaria:

```sql
DROP TABLE IF EXISTS Sapatos.Clientes;

```

O `IF EXISTS` é opcional, mas é uma prática recomendada para evitar erros caso a tabela não exista.

### Passo 3: Confirmar a Deleção

Após executar o comando, você pode listar todas as tabelas no keyspace para verificar se a tabela foi removida corretamente, usando o comando:

```sql
DESCRIBE TABLES;

```

---

# Criar Keyspace

```
CREATE KEYSPACE IF NOT EXISTS Sapatos
WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1};
```

Tabela de clientes:

```
CREATE TABLE Clientes (
    CPF text PRIMARY KEY,
    Nome text,
    Endereco text,
    CEP text,
    Email text,
    Telefones text
);
```

Tabela de Produtos:

```
CREATE TABLE Produtos (
    Codigo int PRIMARY KEY,
    Nome text,
    Modelo text,
    Fabricante text,
    Cor text,
    Tam text
);
```

Tabela de Pedidos:

```
CREATE TABLE Pedidos (
    PedidoID UUID PRIMARY KEY,
    ClienteCPF text,
    Endereco text,
    CEP text,
    Itens list<text>,
    Qtdes list<int>,
    ValorPago decimal
);
```

Observações:

---

- **Chaves Primárias e IDs**: A chave primária para os pedidos é um `UUID`, garantindo a unicidade de cada pedido. Para produtos e clientes, utilizei `codigo` e `cpf`, respectivamente, partindo do pressuposto de que esses campos são únicos.
- **Tipos de Coleção**: As colunas `cor` e `tam` nos produtos e `itens` nos pedidos utilizam tipos de coleção do Cassandra (`LIST` e `MAP`). Esses tipos são adequados para armazenar múltiplos valores em uma única coluna.

---

# Inserindo das nas tabelas

Clientes:

```cassandra
INSERT INTO Clientes.Hapiness (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES('24204365409', 'Tiago Cruz', 'Rua do Oratorio, 520', '14520000', 'tiago.cde@email.com', '19985653625'),
INSERT INTO Clientes.Hapiness (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES('73418177320', 'Zilda Gonzalez', 'Avenida Central, 1200', '35065320', 'zildadbl@email.com', '21958568240'),
INSERT INTO Clientes.Hapiness (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES('74663094097', 'Eduardo Silva', 'Rua estrela da manha, 65', '45262360', 'eduardosil@email.com', '11985634154'),
INSERT INTO Clientes.Hapiness (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES('45678901234', 'Diego Feitosa', 'Praca da arvore, 32', '52657025', 'digdigae@email.com', '48956802054'),
INSERT INTO Clientes.Hapiness (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES('56789012345', 'Andre Luiz', 'Rua da esperança, 202', '58742-000', 'andrezito52@email.com', '11985648000'),
INSERT INTO Clientes.Hapiness (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES('67890123456', 'Julia Mendonça', 'Estrada do pinheiro, 15300', '81526000', 'juliamm@email.com', '11985268432'),
INSERT INTO Clientes.Hapiness (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES('78901234567', 'Carlos Rego', 'Rua Lucio dos gato, 666', '78901234', 'miaumiau@email.com', '11930307070'),
INSERT INTO Clientes.Hapiness (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES('89012345678', 'Eloy Casapequena', 'Estrada do no corredio, 999', '89012345', 'eloyzinho@email.com', '11965413252'),
INSERT INTO Clientes.Hapiness (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES('90123456789', 'Gabriel Soares', 'Rua do piper, 34', '9012000', 'gabshappy@email.com', '52956802154'),
INSERT INTO Clientes.Hapiness (CPF, Nome, Endereco, CEP, Email, Telefones) VALUES('01234567890', 'Elizabeth darcy', 'Avenida Jane Austen, 1820', '32529633', 'elizalovedarcy@email.com', '52985653214');
```

Produtos: 

```
INSERT INTO Produtos.Hapiness (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES('SKU00050', 'Sapato Social', 'Classico', 'Sapatos SA', 'Preto', '40'),
INSERT INTO Produtos.Hapiness (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES('SKU00051', 'Sapato Esportivo', 'Runner', 'Esportivos Ltda', 'Branco', '42'),
INSERT INTO Produtos.Hapiness (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES('SKU00052', 'Sandália Casual', 'Verão', 'Moda Praia', 'Azul', '38'),
INSERT INTO Produtos.Hapiness (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES('SKU00053', 'Bota Trekking', 'Aventura', 'Outdoor Gear', 'Marrom', '41'),
INSERT INTO Produtos.Hapiness (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES('SKU00054', 'Mocassim', 'Confort', 'Elegance Shoes', 'Bege', '39'),
INSERT INTO Produtos.Hapiness (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES('SKU00055', 'Chinelo', 'Simples', 'Conforto SA', 'Verde', '37'),
INSERT INTO Produtos.Hapiness (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES('SKU00056', 'Sapatênis', 'Casual', 'Urbano', 'Cinza', '40'),
INSERT INTO Produtos.Hapiness (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES('SKU00057', 'Tênis Corrida', 'FastRun', 'Speed Shoes', 'Vermelho', '42'),
INSERT INTO Produtos.Hapiness (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES('SKU00058', 'Sapato Casual', 'Dia a Dia', 'Praticidade', 'Preto', '39'),
INSERT INTO Produtos.Hapiness (Codigo, Nome, Modelo, Fabricante, Cor, Tam) VALUES('SKU00059', 'Sandália Esportiva', 'Sporty', 'Adventure', 'Preto', '40');
```

Pedidos:

```
INSERT INTO Pedidos.Hapiness (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES('24204365409', 'Rua do Oratorio, 520', '14520000', '12345678', 'Sapato Social', '1', 299.90),
INSERT INTO Pedidos.Hapiness (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES('73418177320', 'Avenida Central, 1200', '35065320', 'Sapato Esportivo', '2', 699.99),
INSERT INTO Pedidos.Hapiness (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES('74663094097', 'Eduardo Silva', 'Rua estrela da manha, 65', 'Sandália Casual', '1', 59.99),
INSERT INTO Pedidos.Hapiness (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES('45678901234', 'Diego Feitosa', 'Praca da arvore, 32', 'Bota Trekking', '1', 890.00),
INSERT INTO Pedidos.Hapiness (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES('56789012345', 'Andre Luiz', 'Rua da esperança, 202', '58742-000', 'Mocassim', '2', 349.00),
INSERT INTO Pedidos.Hapiness (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES('67890123456', 'Julia Mendonça', 'Estrada do pinheiro, 15300', '81526000', 'Chinelo', '3', 39.90),
INSERT INTO Pedidos.Hapiness (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES('78901234567', 'Carlos Rego', 'Rua Lucio dos gato, 666', '78901234', 'Sapatênis', '1', 279.90),
INSERT INTO Pedidos.Hapiness (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES('89012345678', 'Eloy Casapequena', 'Estrada do no corredio, 999', '89012345', 'Tênis Corrida', '1', 399.90),
INSERT INTO Pedidos.Hapiness (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES('90123456789', 'Gabriel Soares', 'Rua do piper, 34', '9012000', 'Sapato Casual', '2', 559.80),
INSERT INTO Pedidos.Hapiness (ClienteCPF, Endereco, CEP, Itens, Qtdes, ValorPago) VALUES('01234567890', 'Elizabeth darcy', 'Avenida Jane Austen, 1820', '32529633', 'Sandália Esportiva', '1', 249.90);
```

# MongoDB

---

## Utilizando uma Imagem MongoDB no Docker

### Iniciar um Container MongoDB

Para iniciar um container MongoDB previamente criado, utilize o seguinte comando:

```bash
docker exec -it mongodb_sapatos mongosh

```

### Listar Todos os Bancos de Dados

Para listar todos os bancos de dados no MongoDB, use o comando:

```bash
show dbs

```

### Acessar um Banco de Dados

Para acessar um banco de dados específico, use o comando:

```bash
use Sapatos

```

### Deletar um Banco de Dados

Para deletar um banco de dados, siga os passos abaixo:

1. Acesse o banco de dados desejado:
    
    ```bash
    use Sapatos
    
    ```
    
2. Execute o comando para deletar o banco de dados:
    
    ```bash
    db.dropDatabase()
    
    ```
    

### Listar as Coleções de um Banco de Dados

Para listar todas as coleções dentro de um banco de dados, use:

```bash
show collections

```

### Buscar Registros em uma Coleção

Para visualizar os resultados (buscas) de uma coleção específica, use:

```bash
db.nomeDaColecao.find()

```

### Mostrar a Quantidade de Registros em uma Coleção

Para mostrar a quantidade de documentos em uma coleção, utilize:

```bash
db.Produto.countDocuments()

```

---

---

## Configurando MongoDB no Docker

### Baixar a Imagem do Repositório

Para baixar a imagem mais recente do MongoDB do Docker Hub, utilize o seguinte comando:

```bash
docker pull mongo:latest

```

### Criar um Container a partir da Imagem Baixada

Para criar e iniciar um container a partir da imagem do MongoDB, execute:

```bash
docker run -d --name mongodb_sapatos -p 27017:27017 mongo:latest

```

Neste comando:

- `d` executa o container em modo detached (em segundo plano).
- `-name mongodb_sapatos` atribui o nome "mongodb_sapatos" ao container.
- `p 27017:27017` mapeia a porta 27017 do container para a porta 27017 do host.

### Iniciar o MongoDB no Container

Para iniciar uma sessão MongoDB dentro do container, use o comando:

```bash
docker exec -it mongodb_sapatos mongosh

```

---

# Criando Banco de Dados

Criando

```
use Sapatos
```

Criando a colletion Cliente:

```

db.Clientes.insertMany([
    {
        cpf: "24204365409",
        nome: "Tiago Cruz",
        endereco: "Rua do Oratorio, 520",
        cep: "14520000",
        email: "tiago.cde@email.com",
        telefone: "19985653625"
    },
    {
        cpf: "73418177320",
        nome: "Zilda Gonzalez",
        endereco: "Avenida Central, 1200",
        cep: "35065320",
        email: "zildadbl@email.com",
        telefone: "21958568240"
    },
    {
        cpf: "74663094097",
        nome: "Eduardo Silva",
        endereco: "Rua estrela da manha, 65",
        cep: "45262360",
        email: "eduardosil@email.com",
        telefone: "11985634154"
    },
    {
        cpf: "45678901234",
        nome: "Diego Feitosa",
        endereco: "Praca da arvore, 32",
        cep: "52657025",
        email: "digdigae@email.com",
        telefone: "48956802054"
    },
    {
        cpf: "56789012345",
        nome: "Andre Luiz",
        endereco: "Rua da esperança, 202",
        cep: "58742-000",
        email: "andrezito52@email.com",
        telefone: "11985648000"
    },
    {
        cpf: "67890123456",
        nome: "Julia Mendonça",
        endereco: "Estrada do pinheiro, 15300",
        cep: "81526000",
        email: "juliamm@email.com",
        telefone: "11985268432"
    },
    {
        cpf: "78901234567",
        nome: "Carlos Rego",
        endereco: "Rua Lucio dos gato, 666",
        cep: "78901234",
        email: "miaumiau@email.com",
        telefone: "11930307070"
    },
    {
        cpf: "89012345678",
        nome: "Eloy Casapequena",
        endereco: "Estrada do no corredio, 999",
        cep: "89012345",
        email: "eloyzinho@email.com",
        telefone: "11965413252"
    },
    {
        cpf: "90123456789",
        nome: "Gabriel Soares",
        endereco: "Rua do piper, 34",
        cep: "9012000",
        email: "gabshappy@email.com",
        telefone: "52956802154"
    },
    {
        cpf: "01234567890",
        nome: "Elizabeth Darcy",
        endereco: "Avenida Jane Austen, 1820",
        cep: "32529633",
        email: "elizalovedarcy@email.com",
        telefone: "52985653214"
    }
]);

```

Criando a colletion Produto:

```

db.Produtos.insertMany([
    {
        codigo: "SKU00050",
        nome: "Sapato Social",
        modelo: "Classico",
        fabricante: "Sapatos SA",
        cor: "Preto",
        tam: "40"
    },
    {
        codigo: "SKU00051",
        nome: "Sapato Esportivo",
        modelo: "Runner",
        fabricante: "Esportivos Ltda",
        cor: "Branco",
        tam: "42"
    },
    {
        codigo: "SKU00052",
        nome: "Sandália Casual",
        modelo: "Verão",
        fabricante: "Moda Praia",
        cor: "Azul",
        tam: "38"
    },
    {
        codigo: "SKU00053",
        nome: "Bota Trekking",
        modelo: "Aventura",
        fabricante: "Outdoor Gear",
        cor: "Marrom",
        tam: "41"
    },
    {
        codigo: "SKU00054",
        nome: "Mocassim",
        modelo: "Confort",
        fabricante: "Elegance Shoes",
        cor: "Bege",
        tam: "39"
    },
    {
        codigo: "SKU00055",
        nome: "Chinelo",
        modelo: "Simples",
        fabricante: "Conforto SA",
        cor: "Verde",
        tam: "37"
    },
    {
        codigo: "SKU00056",
        nome: "Sapatênis",
        modelo: "Casual",
        fabricante: "Urbano",
        cor: "Cinza",
        tam: "40"
    },
    {
        codigo: "SKU00057",
        nome: "Tênis Corrida",
        modelo: "FastRun",
        fabricante: "Speed Shoes",
        cor: "Vermelho",
        tam: "42"
    },
    {
        codigo: "SKU00058",
        nome: "Sapato Casual",
        modelo: "Dia a Dia",
        fabricante: "Praticidade",
        cor: "Preto",
        tam: "39"
    },
    {
        codigo: "SKU00059",
        nome: "Sandália Esportiva",
        modelo: "Sporty",
        fabricante: "Adventure",
        cor: "Preto",
        tam: "40"
    }
]);
```

Criando a colletion de Pedido:

```
db.Pedidos.insertMany([
    {
        clienteCPF: "24204365409",
        endereco: "Rua do Oratorio, 520",
        cep: "14520000",
        itens: "Sapato Social",
        qtdes: 1,
        valorPago: 299.90
    },
    {
        clienteCPF: "73418177320",
        endereco: "Avenida Central, 1200",
        cep: "35065320",
        itens: "Sapato Esportivo",
        qtdes: 2,
        valorPago: 699.99
    },
    {
        clienteCPF: "74663094097",
        endereco: "Rua estrela da manha, 65",
        cep: "45262360",
        itens: "Sandália Casual",
        qtdes: 1,
        valorPago: 59.99
    },
    {
        clienteCPF: "45678901234",
        endereco: "Praca da arvore, 32",
        cep: "52657025",
        itens: "Bota Trekking",
        qtdes: 1,
        valorPago: 890.00
    },
    {
        clienteCPF: "56789012345",
        endereco: "Rua da esperança, 202",
        cep: "58742-000",
        itens: "Mocassim",
        qtdes: 2,
        valorPago: 349.00
    },
    {
        clienteCPF: "67890123456",
        endereco: "Estrada do pinheiro, 15300",
        cep: "81526000",
        itens: "Chinelo",
        qtdes: 3,
        valorPago: 39.90
    },
    {
        clienteCPF: "78901234567",
        endereco: "Rua Lucio dos gato, 666",
        cep: "78901234",
        itens: "Sapatênis",
        qtdes: 1,
        valorPago: 279.90
    },
    {
        clienteCPF: "89012345678",
        endereco: "Estrada do no corredio, 999",
        cep: "89012345",
        itens: "Tênis Corrida",
        qtdes: 1,
        valorPago: 399.90
    },
    {
        clienteCPF: "90123456789",
        endereco: "Rua do piper, 34",
        cep: "9012000",
        itens: "Sapato Casual",
        qtdes: 2,
        valorPago: 559.80
    },
    {
        clienteCPF: "01234567890",
        endereco: "Avenida Jane Austen, 1820",
        cep: "32529633",
        itens: "Sandália Esportiva",
        qtdes: 1,
        valorPago: 249.90
    }
]);

```

# Cargas - ETAPA 3

[Clientes_novos_hapiness.csv](Trabalho%20em%20Grupo%2001%205e05d5bb6034445a99f102948d4b90d7/Clientes_novos_hapiness.csv)

[Produtos_Novos_Hapiness.csv](Trabalho%20em%20Grupo%2001%205e05d5bb6034445a99f102948d4b90d7/Produtos_Novos_Hapiness.csv)

---

## Fazendo a Carga no MongoDB

### Passo 1: Verificar se `mongoimport` Está Disponível

Primeiro, verifique se o comando `mongoimport` está disponível na sua imagem do Docker. Nem todas as imagens do MongoDB incluem as ferramentas de banco de dados por padrão. Execute o seguinte comando para verificar:

```bash
docker exec -it mongodb_sapatos mongoimport --version

```

Se esse comando falhar, você precisará de uma imagem que inclua as MongoDB Database Tools ou instalar as ferramentas separadamente.

### Passo 2: Colocar o Arquivo CSV Dentro do Container

Para usar o `mongoimport` no Docker, o arquivo CSV precisa estar acessível dentro do container. Copie o arquivo do seu sistema local para o container usando o comando `docker cp`:

```bash
docker cp "C:/arquivos_trabalho/Novos_Produtos_Hapiness.csv" mongodb_sapatos:/Novos_Produtos_MongoDB_UTF8.csv

```

### Passo 3: Executar `mongoimport` no Docker

Depois de copiar o arquivo para o container, execute o `mongoimport` dentro do Docker usando:

```bash
docker exec -it mongodb_sapatos mongoimport --db Sapatos --collection Produto --type csv --file "/Novos_Produtos_Hapiness.csv" --headerline --ignoreBlanks

```

---
