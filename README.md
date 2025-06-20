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
DDL (Data Definition Language)
