# 📚 Projeto Final: Banco de Dados

## 🎯 Objetivo

Este repositório reúne o projeto final da disciplina de **Banco de Dados Relacional**. O objetivo é colocar em prática tudo o que foi aprendido, como:

- Modelagem conceitual e lógica  
- Normalização dos dados  
- Manipulação de dados com comandos:  
  - **DDL** (Data Definition Language)  
  - **DML** (Data Manipulation Language)  
  - **DQL** (Data Query Language)  
  - **DCL** (Data Control Language)  
  - **DTL** (Data Transaction Language)  

---

## 👥 Integrantes do Grupo

- Gizela Alves Pieri Santos  
- Graciele Garglioni  
- Isabelle Nastri Sales  
- Isadora da Silva Zanardo

---

## 📘 Tema Escolhido: Sistema de Gerenciamento de Biblioteca

O sistema foi criado para **gerenciar o cadastro de livros, controlar empréstimos, registrar alunos e organizar o acervo** de uma biblioteca acadêmica.

A proposta permite:
- Organização eficiente dos dados  
- Garantia de integridade e segurança  
- Controle de acesso e permissões  
- Realização de transações seguras

---

## 🧩 Modelagem de Dados

### 🧱 Entidades, Atributos e Relacionamentos

O sistema contempla as seguintes entidades:

- **Biblioteca**: informações sobre campus e acervo  
- **Aluno**: nome, telefone, e-mail, CPF, curso  
- **Livro**: autor, edição, quantidade, status  
- **Empréstimo**: relaciona clientes, livros e bibliotecas  

### 🔗 Diagrama Entidade-Relacionamento (DER)

Relação entre alunos, faculdades, bibliotecas e controle de empréstimos.

![Modelagem](./docs/modelagem.jpeg)

---

## 🧮 Normalização

O banco de dados foi organizado até a **Terceira Forma Normal (3FN)**:

- **1FN**: dados simples (sem repetições)  
- **2FN**: dependências corretamente vinculadas  
- **3FN**: eliminação de dependências transitivas  

---

## 📂 Scripts SQL

### 📁 DDL – *Data Definition Language*

Local: `sql/ddl.sql`

```sql
CREATE TABLE bibilioteca (
  id SERIAL PRIMARY KEY,
  nome_campus VARCHAR(50),
  data_emprestimo DATE,
  data_devoluvao DATE
);

CREATE TABLE cliente (
  cliente_id SERIAL PRIMARY KEY,
  foto VARCHAR(20),
  cpf VARCHAR(11),
  nome VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE,
  telefone VARCHAR(20),
  curso VARCHAR(20)
);

CREATE TABLE livro (
  codigo_id SERIAL PRIMARY KEY,
  autor VARCHAR(100),
  ano_data DATE,
  edicao VARCHAR(50),
  quantidade_livro NUMERIC(10,1) NOT NULL,
  status_do_aluguel VARCHAR(100),
  idioma VARCHAR(50),
  gênero VARCHAR(20)
);

CREATE TABLE empréstimo (
  emprestimo_id SERIAL PRIMARY KEY,
  cliente_id INT REFERENCES cliente(cliente_id),
  codigo_id INT REFERENCES livro(codigo_id),
  biblioteca_id INT REFERENCES bibilioteca(id)
);

---

### 📁 DML - *Data Manipulation Language*

Local: `sql/dml.sql`

-- Inserções
INSERT INTO aluno (telefone, email, cpf, semestre, curso, foto, registro_ra, nome, id_aluno)
VALUES ('(11)99999-0000', 'isazanardi@gmail.com', '11000000', 'semestre 2', 'Ads', 'fotoq1.jpg', 0000, 'Isadora', 09);

INSERT INTO livro (genero, idioma, quantidade, status, edicao, ano, autor, patrimonio, id_livro)
VALUES ('Romance', 'Português', 10, 'Disponível', '2ª', 2020, 'Machado de Assis', 'BR12345', 1);

INSERT INTO bibilioteca (quant_livros, unidades, id_biblioteca)
VALUES (1500, 'Campus Centro', 1);

INSERT INTO faculdade (contato, endereco, cnpj, materias, alunos, funcionarios, cursos, campus, id_faculdade)
VALUES ('(11) 4002-8922', 'Rua das Flores, 123 - São Paulo, SP', '12.345.678/0001-90', 35, 1200, 80, 10, 'Centro', 1);

INSERT INTO emprestimo (cliente_id, codigo_id, biblioteca_id)
VALUES (1, 1, 1);

-- Atualizações
UPDATE cliente
SET telefone = '(11)98888-7777'
WHERE cliente_id = 1;

UPDATE livro
SET quantidade_livro = 9
WHERE codigo_id = 1;

UPDATE biblioteca
SET nome_campus = 'Campus Sul'
WHERE id = 1;

-- Exclusões
DELETE FROM emprestimo WHERE emprestimo_id = 1;
DELETE FROM cliente WHERE cliente_id = 1;
DELETE FROM livro WHERE codigo_id = 1;
DELETE FROM biblioteca WHERE id = 1;

---

### 📁 DQL - *Data Quey Language*

Local: `sql/dql.sql`

SELECT * FROM cliente;

SELECT * FROM livro
WHERE status_do_aluguel = 'Disponível';

SELECT
  e.emprestimo_id,
  c.nome AS nome_cliente,
  l.autor AS autor_livro,
  b.nome_campus AS biblioteca
FROM emprestimo e
JOIN cliente c ON e.cliente_id = c.cliente_id
JOIN livro l ON e.codigo_id = l.codigo_id
JOIN bibilioteca b ON e.biblioteca_id = b.id;

SELECT SUM(quantidade_livro) AS total_livros FROM livro;

SELECT DISTINCT c.nome
FROM cliente c
JOIN emprestimo e ON c.cliente_id = e.cliente_id;

SELECT c.nome, COUNT(e.emprestimo_id) AS livros_emprestados
FROM cliente c
JOIN emprestimo e ON c.cliente_id = e.cliente_id
GROUP BY c.nome;

---

### 📁 DCL - *Data Control Language*

Local: `sql/dcl.sql`

-- Criação de usuários
CREATE USER bibliotecario IDENTIFIED BY 'senha123';
CREATE USER leitor IDENTIFIED BY 'senha456';

-- Permissões
GRANT SELECT, INSERT, UPDATE, DELETE ON livros TO bibliotecario;
GRANT SELECT ON livros TO leitor;

-- Revogação
REVOKE DELETE ON livros FROM bibliotecario;

-- Verificação
SHOW GRANTS FOR bibliotecario;
SHOW GRANTS FOR leitor;

---

### 📁 DTL - *Data Transaction Language*

Local: `sql/dtl.sql`

-- Função para registrar empréstimo
CREATE OR REPLACE FUNCTION registrar_emprestimo(...)
RETURNS TEXT AS $$
BEGIN
  -- lógica do empréstimo
END;
$$ LANGUAGE plpgsql;

-- Função para registrar devolução
CREATE OR REPLACE FUNCTION registrar_devolucao(...)
RETURNS TEXT AS $$
BEGIN
  -- lógica da devolução
END;
$$ LANGUAGE plpgsql;
