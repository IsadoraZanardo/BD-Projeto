Projeto Final: Banco de Dados Relacional
Objetivo
Este repositório reúne o projeto final da disciplina de Banco de Dados Relacional. O objetivo é colocar em prática tudo o que foi aprendido, como a modelagem conceitual e lógica, a normalização e a manipulação de dados usando comandos DDL, DML e DQL. Além disso, há uma atenção especial para comandos DCL e DTL.

Integrantes do Grupo
Gizela Alves Pieri Santos
Graciele Garglioni
Isabelle Nastri Sales
Isadora da Silva Zanardo

Tema Escolhido
Sistema de Gerenciamento de Biblioteca
Este sistema foi criado para ajudar a gerenciar o cadastro de livros, controlar empréstimos, registrar os alunos e organizar os acervos de uma biblioteca acadêmica. Com ele, você pode colocar em prática conceitos importantes de bancos de dados relacionais, como organizar os dados de forma eficiente, garantir que as informações estejam corretas e seguras, além de controlar quem tem acesso a cada recurso e realizar transações de forma segura.
Este repositório contém o projeto final da disciplina de Banco de Dados Relacional. O objetivo é aplicar tudo o que foi estudado, incluindo a modelagem conceitual e lógica, a normalização dos dados e a manipulação das informações usando comandos como DDL, DML, DQL e também comandos adicionais como DCL e DTL, que trazem funcionalidades extras para o gerenciamento do banco.

Modelagem de Dados
Entidades, Atributos e Relacionamentos
O sistema contempla as seguintes entidades:
Biblioteca: Contém informações sobre as unidades e o acervo.
Aluno: Registro de alunos com atributos como nome, telefone, e-mail, CPF, curso.
Livro: Cadastro de livros com informações como autor, edição, quantidade e status.
Empréstimo: Relaciona clientes, livros e bibliotecas, registrando os empréstimos realizados.
Diagrama Entidade-Relacionamento (DER)
O modelo DER inclui a relação entre alunos, faculdades, bibliotecas e controle de empréstimos de livros.
![modelagem](./docs/modelagem.jpeg)

Normalização
O banco de dados foi organizado até a Terceira Forma Normal (3FN), o que garante uma estrutura mais eficiente e confiável. Na Primeira Forma Normal (1FN), todos os dados foram divididos em valores simples, ou seja, cada campo tem apenas uma informação. Na Segunda Forma Normal (2FN), todas as dependências que não envolvem a chave principal foram corretamente vinculadas às chaves primárias, evitando repetições desnecessárias. Por fim, na Terceira Forma Normal (3FN), foram eliminadas as dependências transitivas, ajudando a manter a integridade e a eficiência do banco de dados.

Scripts SQL
Todos os scripts estão localizados na pasta /sql.
DDL (Data Definition Language):
--create
create table bibilioteca( id serial primary key,
nome_campus varchar(50), data_emprestimo date, data_devoluvao date
);
--create
create table cliente( cliente_id serial primary key, foto varchar(20),
cpf varchar(11),
nome varchar(100)not null, email varchar(100) unique, telefone varchar(20), curso varchar(20)
);
--create
create table livro(
codigo_id serial primary key, autor varchar(100), ano_data date,
edicao varchar(50),
quantidade_livro numeric(10,1) not null, status_do_aluguel varchar(100), idioma varchar (50),
Gênero varchar(20)
);
-- create: tabela que relaciona clientes, livros e registros de empréstimo create table empréstimo (
emprestimo_id serial primary key, cliente_id int references cliente(cliente_id), codigo_id int references livro(codigo_id),
biblioteca_id int references bibilioteca(id)
);
Caminho: sql/ddl.sql

DML
-- Inserir clientes
INSERT INTO aluno (telefone, email, cpf, semestre, curso, foto, registro_ra, nome, id_aluno)
VALUES (‘(11)99999-0000’, 'isazanardi@gmail.com', ‘11000000’, 'semestre 2', 'Ads',
'fotoq1.jpg', 0000, ‘Isadora’, 09);
-- Inserir livros
INSERT INTO livro (genero, idioma, quantidade, status, edicao, ano, autor, patrimonio, id_livro)
VALUES ('Romance', 'Português', 10, 'Disponível', '2ª', 2020, 'Machado de Assis', 'BR12345', 1);
-- Inserir biblioteca
INSERT INTO bibilioteca (quant_livros, unidades, id_biblioteca) VALUES (1500, 'Campus Centro', 1);
- - Inserir Faculdade
INSERT INTO faculdade (contato, endereco, cnpj, materias, alunos, funcionarios, cursos, campus, id_faculdade)
VALUES ('(11) 4002-8922', 'Rua das Flores, 123 - São Paulo, SP', '12.345.678/0001-90', 35, 1200, 80, 10, 'Centro', 1);
-- Inserir empréstimo
INSERT INTO emprestimo (cliente_id, codigo_id, biblioteca_id) VALUES (1, 1, 1);
Atualização de Registros (UPDATE):
UPDATE cliente
SET telefone = '(11)98888-7777'
WHERE cliente_id = 1;
-- Atualizar a quantidade de livros disponíveis
UPDATE livro
SET quantidade_livro = 9
WHERE codigo_id = 1;
-- Atualizar o nome do campus da biblioteca
UPDATE biblioteca
SET nome_campus = 'Campus Sul'
WHERE id = 1;
Exclusão de Registros:
-- Excluir um empréstimo específico
DELETE FROM emprestimo
WHERE emprestimo_id = 1;
-- Excluir um cliente
DELETE FROM cliente
WHERE cliente_id = 1;
-- Excluir um livro
DELETE FROM livro
WHERE codigo_id = 1;
-- Excluir uma biblioteca
DELETE FROM biblioteca
WHERE id = 1;
Caminho: sql/dml.sql

DQL
Listar todos os clientes cadastrados:
SELECT * FROM cliente;
SELECT * FROM livro
WHERE status_do_aluguel = 'Disponível';
Mostrar	os	dados	de	todos	os	empréstimos: SELECT
e.emprestimo_id,
c.nome AS nome_cliente, l.autor AS autor_livro, b.nome_campus AS biblioteca
FROM
emprestimo e
JOIN cliente c ON e.cliente_id = c.cliente_id JOIN livro l ON e.codigo_id = l.codigo_id JOIN bibilioteca b ON e.biblioteca_id = b.id;
Quantidade	total	de	livros	cadastrados: SELECT SUM(quantidade_livro) AS total_livros FROM livro;
Ver	todos	os	clientes	que	já	realizaram	algum	empréstimo: SELECT DISTINCT c.nome
FROM cliente c
JOIN emprestimo e ON c.cliente_id = e.cliente_id;
Mostrar	a	quantidade	de	livros	emprestados	por	cliente: SELECT c.nome, COUNT(e.emprestimo_id) AS livros_emprestados
FROM cliente c
JOIN emprestimo e ON c.cliente_id = e.cliente_id GROUP BY c.nome;
Caminho: sql/dql.sql

DCL:
-- Criação de Usuários
CREATE USER bibliotecario IDENTIFIED BY 'senha123'; CREATE USER leitor IDENTIFIED BY 'senha456';
-- Atribuição de Permissões
GRANT SELECT, INSERT, UPDATE, DELETE ON livros TO bibliotecario; GRANT SELECT ON livros TO leitor;
-- Revogação de Permissões
REVOKE DELETE ON livros FROM bibliotecario;
-- Verificação de Permissões SHOW GRANTS FOR bibliotecario; SHOW GRANTS FOR leitor;
Caminho: sql/dcl.sql

DTL:
Função para registrar empréstimo
CREATE OR REPLACE FUNCTION registrar_emprestimo( p_livro_id INT,
p_membro_id INT, p_data_emprestimo DATE, p_data_devolucao_prevista DATE
)
RETURNS TEXT AS $$ DECLARE
v_quantidade_disponivel INT; BEGIN
-- Verifica a quantidade disponível
SELECT quantidade_disponivel INTO v_quantidade_disponivel FROM livros
WHERE id_livro = p_livro_id;
IF v_quantidade_disponivel > 0 THEN
-- Atualiza quantidade UPDATE livros
SET quantidade_disponivel = quantidade_disponivel - 1 WHERE id_livro = p_livro_id;
-- Insere empréstimo
INSERT	INTO	emprestimos	(id_livro,	id_membro,	data_emprestimo, data_devolucao_prevista, status)
VALUES	(p_livro_id,	p_membro_id,	p_data_emprestimo, p_data_devolucao_prevista, 'EMPRESTADO');
RETURN 'Empréstimo registrado com sucesso!'; ELSE
RETURN 'Não há livros disponíveis.';
 
END IF; END;
$$ LANGUAGE plpgsql;
-- Exemplo de chamada correta (fora da função):
-- BEGIN;
-- SELECT registrar_emprestimo(1, 1, '2025-05-30', '2025-06-04');
-- COMMIT;
-- Função para registrar devolução
CREATE OR REPLACE FUNCTION registrar_devolucao( p_emprestimo_id INT,
p_data_devolucao DATE
)
RETURNS TEXT AS $$ DECLARE
v_livro_devolvido_id INT; v_rows_updated INT;
BEGIN
-- Atualiza o empréstimo se ainda não foi devolvido UPDATE emprestimos
SET
status = 'DEVOLVIDO', data_devolucao = p_data_devolucao
WHERE
id_emprestimo = p_emprestimo_id AND status = 'EMPRESTADO'
RETURNING id_livro INTO v_livro_devolvido_id; IF FOUND THEN
-- Atualiza a quantidade de livros disponíveis UPDATE livros
SET quantidade_disponivel = quantidade_disponivel + 1
 
WHERE id_livro = v_livro_devolvido_id; RETURN 'Devolução registrada com sucesso!';
ELSE
RETURN 'Empréstimo não encontrado ou já devolvido.'; END IF;
EXCEPTION
WHEN OTHERS THEN
RETURN 'Ocorreu um erro ao registrar a devolução: ' || SQLERRM; END;
$$ LANGUAGE plpgsq

Caminho: sql/dtl.sql
