UniversidadeDB

Tabelas cursos: Esta tabela armazena os cursos oferecidos pela universidade.

id: Identificador único do curso (chave primária). nome: Nome do curso. alunos Nesta tabela são registrados os alunos matriculados na universidade.

RA: Registro Acadêmico, identificador único do aluno (chave primária). nome: Nome do aluno. sobrenome: Sobrenome do aluno. cursoaluno: Chave estrangeira referenciando o curso que o aluno está cursando. universidade: Chave estrangeira referenciando a universidade em que o aluno está matriculado. professor A tabela de professores armazena informações sobre os professores da universidade.

id: Identificador único do professor (chave primária). nome: Nome do professor. email: Endereço de email do professor. cursoprofessor: Chave estrangeira referenciando o curso que o professor leciona. universidade: Chave estrangeira referenciando a universidade em que o professor leciona. universidade Esta tabela contém informações sobre as universidades.

id: Identificador único da universidade (chave primária). nome: Nome da universidade. endereco: Endereço da universidade. EmailsAlunos Essa tabela é responsável por armazenar os emails dos alunos.

id: Identificador único do email (chave primária). email: Endereço de email do aluno.

Procedimentos Armazenados criar_email_aluno Este procedimento armazenado é utilizado para gerar automaticamente o endereço de email de um aluno, seguindo o formato nome.sobrenome@dominio.com Este tipo de armazenamento serve para facilitar e automatizar a criação de um email de alunos e suas faculdades. Caso tenham duas pessoas com mesmo nome e sobre nome seus emails ficarão iguais.

Parâmetros: nomeprocedure: Nome do aluno. sobreprocedure: Sobrenome do aluno. uniprocedure: Nome da universidade para compor o domínio do email.

Código em MySQL:

create database universidadedb; use universidadedb;

CREATE TABLE cursos ( id INTEGER PRIMARY KEY AUTO_INCREMENT, nome VARCHAR(100) );

INSERT INTO cursos (nome) VALUES ('Matemática'), ('História'), ('Biologia'), ('Literatura'), ('Física'), ('Química'), ('Geografia'), ('Inglês'), ('Artes');

CREATE TABLE alunos ( RA INTEGER PRIMARY KEY AUTO_INCREMENT, nome VARCHAR(60), sobrenome VARCHAR(60), cursoaluno INTEGER, universidade INTEGER,

FOREIGN KEY (cursoaluno) REFERENCES cursos(id),
FOREIGN KEY (universidade) REFERENCES universidade(id)
);

INSERT INTO alunos (nome, sobrenome, cursoaluno, universidade) VALUES ('João ', 'silva', 1, 1),

('Maria ', 'santos', 2, 2),

('Pedro ', 'oliveira', 3, 3),

('Ana', 'souza', 4, 4),

('Carlos', 'ferreira', 5, 5),

('Luana', 'pereira', 6, 6),

('Mariana', 'costa', 7, 2),

('José', 'santos', 8, 1),

('Amanda', 'lima', 9, 3);

CREATE TABLE professor ( id INTEGER PRIMARY KEY AUTO_INCREMENT, nome VARCHAR(60), email VARCHAR(60), cursoprofessor INTEGER, universidade INTEGER,

FOREIGN KEY (cursoprofessor) REFERENCES cursos(id),
FOREIGN KEY (universidade) REFERENCES universidade(id)
);

INSERT INTO professor (nome, email, cursoprofessor, universidade) VALUES ('Carlos Oliveira', 'carlos@gmail.com', 1, 2),

('Ana Rodrigues', 'ana@gmail.com', 2, 3),

('Pedro Almeida', 'pedro@gmail.com', 3, 4),

('Mariana Lima', 'mariana@gmail.com', 4, 5),

('Luana Pereira', 'luana@gmail.com', 5, 6),

('José Ferreira', 'jose@gmail.com', 6, 3),

('Amanda Costa', 'amanda@gmail.com', 7, 4),

('Fernanda Silva', 'fernanda@gmail.com', 8, 5),

('Rafael Santos', 'rafael@gmail.com', 9, 2),

('Daniel Ohata', 'Daniel.ohata@facens.com', 1, 1);

CREATE TABLE universidade ( id INTEGER PRIMARY KEY AUTO_INCREMENT, nome VARCHAR(100), endereco VARCHAR(255)
);

INSERT INTO universidade (nome, endereco) VALUES ('FACENS', 'Rodovia Senador José Ermírio de Moraes, 1425 - Alto da Boa Vista, Sorocaba, SP'),

('Universidade Federal do Rio de Janeiro', 'Av. Pedro Calmon, 550 - Cidade Universitária, Rio de Janeiro, RJ'),

('Universidade de São Paulo', 'Av. Prof. Mello Moraes, 65 - Butantã, São Paulo, SP'),

('Universidade Federal de Minas Gerais', 'Av. Antônio Carlos, 6627 - Pampulha, Belo Horizonte, MG'),

('Universidade Estadual de Campinas', 'Av. Érico Veríssimo, 2500 - Cidade Universitária, Campinas, SP'),

('Universidade Federal do Rio Grande do Sul', 'Av. Paulo Gama, 110 - Farroupilha, Porto Alegre, RS');

create table EmailsAlunos( id int primary key auto_increment, email varchar(255) );

DELIMITER //

CREATE PROCEDURE criar_email_aluno(IN nomeprocedure VARCHAR(100),IN sobreprocedure varchar(100),IN uniprocedure varchar(100)) BEGIN DECLARE email1 VARCHAR(255);

DECLARE nome1 	 VARCHAR(255);

DECLARE nome2	 VARCHAR(255);

DECLARE nomeuni  varchar(255);



SET nome1 = nomeprocedure;

SET nome2 = sobreprocedure;

SET nomeuni = uniprocedure;

SET email1 = CONCAT(nome1, '.', nome2, '@', nomeuni, '.com');

INSERT INTO EmailsAlunos(email) VALUES (email1);

SELECT * FROM EmailsAlunos;
END; //

DELIMITER ;

call criar_email_aluno('João','silva','FACENS'); select * from EmailsAlunos;
