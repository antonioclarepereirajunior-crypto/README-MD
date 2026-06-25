
# Sistema de Gerenciamento de Biblioteca

## Descrição do Projeto

O Sistema de Gerenciamento de Biblioteca foi desenvolvido com o objetivo de aplicar conceitos de Programação Orientada a Objetos (POO), Persistência de Dados, Arquitetura em Camadas e Banco de Dados Relacional utilizando PostgreSQL.

O sistema permite o gerenciamento completo de bibliotecas, usuários, livros e empréstimos, simulando operações reais de controle de acervo, empréstimo e devolução de exemplares.

Além da modelagem orientada a objetos, o projeto utiliza o padrão DAO (Data Access Object) para acesso aos dados e Maven para gerenciamento de dependências.

---

## Objetivos

Desenvolver uma aplicação capaz de:

* Gerenciar bibliotecas e seus acervos;
* Cadastrar e controlar usuários;
* Realizar empréstimos e devoluções de livros;
* Garantir integridade dos dados por meio de regras de negócio;
* Aplicar conceitos de Programação Orientada a Objetos;
* Implementar persistência de dados com PostgreSQL;
* Utilizar o padrão DAO para separação entre regras de negócio e acesso ao banco de dados;
* Utilizar Maven para gerenciamento do projeto e dependências.

---

## Funcionalidades Implementadas

### Gestão de Bibliotecas

* Cadastro de bibliotecas;
* Alteração e remoção de registros;
* Consulta de bibliotecas cadastradas;
* Associação de livros ao acervo.

### Gestão de Livros

* Cadastro de livros;
* Consulta por título, autor e gênero;
* Controle automático de disponibilidade;
* Associação a uma biblioteca.

### Gestão de Usuários

* Cadastro de usuários;
* Controle de CPF e e-mail únicos;
* Consulta e atualização de dados;
* Registro automático da data de cadastro.

### Gestão de Empréstimos

* Registro de empréstimos;
* Controle de devoluções;
* Histórico completo;
* Atualização automática do status dos livros.

### Consultas

* Livros por gênero;
* Livros por autor;
* Livros por faixa de páginas;
* Empréstimos ativos;
* Histórico de empréstimos.

---

## Arquitetura do Projeto

O sistema foi organizado seguindo uma arquitetura em camadas:

### Camada de Entidades

Responsável por representar os objetos do sistema:

* Biblioteca
* Livro
* Usuario
* Emprestimo

### Camada DAO

Responsável pelas operações de acesso ao banco de dados:

* BibliotecaDAO
* LivroDAO
* UsuarioDAO
* EmprestimoDAO

Principais operações:

* Inserir registros;
* Atualizar registros;
* Excluir registros;
* Consultar registros;
* Buscar registros por filtros.

O uso do padrão DAO permite maior organização, manutenção e reutilização do código.

### Camada de Conexão

Responsável pela comunicação com o PostgreSQL através do JDBC.

Classe principal:

* ConnectionFactory

Funções:

* Abrir conexão;
* Fechar conexão;
* Centralizar configurações do banco de dados.

---

## Modelagem Orientada a Objetos

### Biblioteca

#### Atributos

* idBiblioteca
* nome
* endereco
* telefone

#### Relacionamentos

* Uma biblioteca possui vários livros;
* Uma biblioteca possui vários empréstimos.

---

### Livro

#### Atributos

* idLivro
* titulo
* autor
* genero
* numeroPaginas
* status

#### Relacionamentos

* Pertence a uma biblioteca;
* Participa de empréstimos.

---

### Usuario

#### Atributos

* idUsuario
* nome
* cpf
* email
* telefone
* dataCadastro

#### Relacionamentos

* Pode realizar vários empréstimos.

---

### Emprestimo

#### Atributos

* idEmprestimo
* dataEmprestimo
* dataPrevistaDevolucao
* dataDevolucao
* statusEmprestimo

#### Relacionamentos

* Relacionado a usuário;
* Relacionado a livro;
* Relacionado a biblioteca.

---

## Regras de Negócio

### Disponibilidade de Livros

Um livro só poderá ser emprestado se estiver disponível.

Ao realizar um empréstimo:

status = EMPRESTADO

Ao realizar uma devolução:

status = DISPONIVEL

### Controle de Empréstimos

* Todo empréstimo deve possuir usuário válido;
* Todo empréstimo deve possuir livro válido;
* Todo empréstimo deve possuir biblioteca válida;
* A devolução não pode ocorrer antes da data de empréstimo.

### Integridade dos Dados

* CPF único;
* E-mail único;
* Chaves primárias para todas as entidades;
* Chaves estrangeiras para relacionamentos.

---

## Banco de Dados

O sistema utiliza PostgreSQL como Sistema Gerenciador de Banco de Dados.

### Tabelas

#### biblioteca

Armazena os dados das bibliotecas.

#### usuario

Armazena os usuários cadastrados.

#### livro

Armazena os livros do sistema.

#### emprestimo

Armazena empréstimos e devoluções.

---

## Conexão com Banco de Dados

A conexão é realizada utilizando JDBC.

Exemplo de configuração:

```java
private static final String URL =
"jdbc:postgresql://localhost:5432/biblioteca";

private static final String USER = "postgres";
private static final String PASSWORD = "123456";
```

A conexão é gerenciada pela classe ConnectionFactory, responsável por disponibilizar conexões para os DAOs.

---

## Maven

O projeto utiliza Maven para gerenciamento das dependências.

### Dependência PostgreSQL

```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.7.3</version>
</dependency>
```

### Benefícios do Maven

* Gerenciamento automático de bibliotecas;
* Organização do projeto;
* Facilidade de compilação;
* Padronização da estrutura de diretórios.

---

## Tecnologias Utilizadas

### Linguagem

* Java

### Banco de Dados

* PostgreSQL

### Persistência

* JDBC
* DAO

### Gerenciamento

* Maven

### Conceitos Aplicados

* Programação Orientada a Objetos
* Encapsulamento
* Herança
* Polimorfismo
* CRUD
* Integridade Referencial
* Banco de Dados Relacional
* Arquitetura em Camadas

### Ferramentas

* Eclipse IDE
* PostgreSQL
* Maven
* Git
* GitHub
* Excalidraw

---

## Estrutura do Projeto

```text
ProjetoBiblioteca
│
├── src/main/java
│
├── entidade
│   ├── Biblioteca.java
│   ├── Livro.java
│   ├── Usuario.java
│   └── Emprestimo.java
│
├── dao
│   ├── BibliotecaDAO.java
│   ├── LivroDAO.java
│   ├── UsuarioDAO.java
│   └── EmprestimoDAO.java
│
├── connection
│   └── ConnectionFactory.java
│
├── App.java
│
├── src/main/resources
│
├── pom.xml
│
├── trabalhoBN.sql
├── excalidraw.png
└── README.md
```

---

## Aprendizados Obtidos

Durante o desenvolvimento do projeto foram aplicados conhecimentos relacionados a:

* Programação Orientada a Objetos;
* Persistência de dados com JDBC;
* Utilização do padrão DAO;
* Integração Java com PostgreSQL;
* Criação de CRUD completo;
* Modelagem de banco de dados relacional;
* Utilização de Maven;
* Organização de projetos em camadas.

---

## Considerações Finais

O Sistema de Gerenciamento de Biblioteca integra conceitos de Programação Orientada a Objetos, Banco de Dados Relacional e Persistência de Dados, simulando um ambiente real de gerenciamento de acervo.

A utilização de PostgreSQL, JDBC, DAO e Maven torna o projeto mais próximo das práticas utilizadas no mercado de desenvolvimento de software, proporcionando uma experiência completa de aprendizado.

---

## Autor

Projeto desenvolvido para fins acadêmicos na disciplina de Desenvolvimento de Sistemas.
