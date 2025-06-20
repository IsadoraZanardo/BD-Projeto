# 📚 Projeto Final: Banco de Dados Relacional

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

