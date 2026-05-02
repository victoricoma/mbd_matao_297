# PLANO DE AULA

Candidato(a): Victor Sena Icoma
Concurso: Professor de Ensino Superior – Fatec Matão (Edital Nº 297/01/2026)
Curso: Superior de Tecnologia em Desenvolvimento de Software Multiplataforma
Disciplina: Modelagem de Banco de Dados
Tema da Aula: Modelagem Conceitual de Banco de Dados: Entidades, Atributos, Relacionamentos e Cardinalidades
Duração: 50 minutos

## 1. OBJETIVOS

Objetivo Geral:
Capacitar os alunos a abstrair requisitos do mundo real e representá-los graficamente através do Modelo Entidade-Relacionamento (MER).

## Objetivos Específicos:

Compreender o propósito do nível conceitual na arquitetura de bancos de dados.

Identificar e diagramar corretamente Entidades e Atributos a partir de um cenário prático.

Estabelecer Relacionamentos entre entidades.

Analisar e definir Cardinalidades (mínima e máxima) com base em regras de negócio.

## 2. CONTEÚDO PROGRAMÁTICO

Introdução à Modelagem Conceitual: O que é e por que é independente de SGBD.

Entidades: Definição, notação gráfica, Entidades Fortes vs. Entidades Fracas.

Atributos: Simples, Compostos, Multivalorados e Determinantes (Chaves).

Relacionamentos: Associação entre instâncias, grau de relacionamento.

Cardinalidades: Regras de negócio, restrição de participação (mínima) e de proporção (máxima) - Notação (1,1), (0,n), etc.

## 3. METODOLOGIA E ESTRATÉGIAS DIDÁTICAS

A aula será conduzida através de Exposição Dialogada e Problematização.

Fase Teórica: Apresentação dos conceitos fundamentados na literatura clássica com exemplos cotidianos (ex: Sistema de uma Faculdade).

Fase Prática (Construção Conjunta): Resolução de um Estudo de Caso ("Mini-Mundo" de um E-commerce) sendo modelado passo a passo na lousa, simulando a extração de requisitos juntamente com a turma para fixação imediata do aprendizado.

## 4. RECURSOS DIDÁTICOS

GitHub e Readme com Lousa e Prática Laboratorial e Mapamental com STEAM.

Projetor Multimídia (slides esquemáticos para definições formais).

Opcional: Demonstração de uma ferramenta CASE de modelagem conceitual (ex: brModelo).

## 5. AVALIAÇÃO

A avaliação será do tipo Formativa e Contínua:

Observação da participação dos alunos durante a modelagem conjunta na lousa.

Resolução de um "Quiz rápido" oral ao final da aula sobre restrições de cardinalidade.

Como atividade extraclasse, será proposto um descritivo de negócio (Sistema de Biblioteca) para que os alunos entreguem o respectivo DER na próxima aula.

## 6. BIBLIOGRAFIA DE REFERÊNCIA

Básica: HEUSER, Carlos A. Projeto de Banco de Dados. 6 ed. Porto Alegre: Bookman, 2010.

Básica: ELMASRI, R.; NAVATHE, S. B. Sistemas de Banco de Dados: Fundamentos e Aplicações. 7 ed. São Paulo: Pearson, 2019.

<hr>

# Aulas de MySQL

<img width="857" height="350" alt="image" src="https://github.com/user-attachments/assets/e54c3ce1-fbf2-4c32-af39-0c5e9d255205" />



## DER do Banco

<img width="1037" height="589" alt="image" src="https://github.com/user-attachments/assets/bde331dd-aaac-4bb6-98ce-ea02bd755878" />



# Tabelas e Entidades

<HR>

   ```sh
  create database empregados_db;
use empregados_db;

create table departamento(
	cod_depto int auto_increment not null unique,
    nome varchar(100) not null,
    constraint primary key(cod_depto) 
);
create table empregado(
	cod_emp int not null auto_increment unique,
    cod_depto int not null,
    nome varchar(100) not null,
    dt_nascimento date not null,
    sexo char(1),
    dt_admissao date not null,
    civil char(1),
    salario decimal(10, 2) not null,
    constraint primary key(cod_emp),
    constraint fk_depto_emp foreign key(cod_depto) references departamento(cod_depto)
);
create table dependente(
	cod_dep int not null auto_increment,
    cod_emp int,
    nome varchar(100),
    dt_nascimento date,
    sexo char(1),
    constraint primary key (cod_dep, cod_emp),
    constraint fk_emp_dep foreign key (cod_emp) references empregado(cod_emp)
);
   ```
# Inserts para Querys de Prática
   ```sh
insert into departamento(nome) values('Informática');
insert into departamento(nome) values('Recursos Humanos');
insert into departamento(nome) values('Desenvolvimento');
insert into departamento(nome) values('Diretoria');
insert into departamento(nome) values('Marketing');
insert into departamento(nome) values('Qualidade');

insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'CARLOS DA SILVEIRA MELO','1973-06-02','M','1994-05-20','C',3200);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(1,'FÁBIO MELO','2013-10-15','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(1,'KARINA MELO','2022-02-12','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(3,'ROBERTO RAMALHO','1981-10-15','M','1998-05-07','C',4600);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(2,'AMANDA RAMALHO','2013-06-10','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(2,'LAYS RAMALHO','2010-06-09','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(2,'LUCAS RAMALHO','2010-02-14','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'NATHAN FARCCA','1984-06-30','M','1990-05-12','S',5300);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(3,'FRANCINE MOTTA FARCCA','2009-08-12','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(3,'LINDIANE MOTTA FARCCA','2020-06-15','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(3,'ENZO MOTTA FARCCA','2021-07-03','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'MELANI CARVALHO','1970-08-12','F','1999-04-20','S',12000);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(4,'MARCOS CARVALHO NETO','2010-01-25','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'ANA CARLA MENINO','1963-12-22','F','2003-02-21','V',24000);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(4,'ANALDER MENINO','1999-01-01','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'CARLOS PETTRA','1985-11-18','M','2005-02-19','S',3500);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(5,'LUAN ANTONIO PETTRA','2010-12-25','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'CIRLO SENA','1985-12-22','M','2003-08-20','C',2400);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(6,'ANTONI SENA FILHO','2011-09-09','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(2,'CARLOS KITAYMA','1985-03-30','M','2002-12-20','C',3600);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(6,'LEONARDO MARCOS SENA','2005-11-08','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(2,'MARCOS MAEMURA','1981-07-09','M','2005-11-01','V',4500);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(4,'ALINE MAEUMURA','2006-08-17','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'JOÃO ROBERTO BAIRRO','1984-10-10','M','2001-05-02','C',4500);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(8,'GISELE KITAYMA','2009-02-16','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(8,'MARCOS KITAYMA','2004-02-02','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(3,'SILVIO MORGATO','1966-06-10','M','1997-05-02','C',4800);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(8,'TALIA BAIRRO','2014-03-02','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(8,'ANIA BAIRRO','1973-03-30','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(2,'ANA CARVALHO FERREIRA','1977-08-15','F','1994-03-20','V',5200);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(10,'JOÃO FRANCISCO MORGATO','2012-03-30','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'ANTONIO MARCONATO','1979-09-26','M','1992-05-02','V',7500);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(11,'ALLIAN PEREIRA MATOS','2011-03-03','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'ANTONIO SINTALA','1973-03-02','M','1992-05-18','D',8500);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(12,'CLARICE MARCONATO','2011-10-08','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(3,'MARIA FELÍCIA MARCELINO','1979-02-12','F','1993-02-26','C',6900);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(13,'MARCOS VINICIUS SINTALA','2013-11-08','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(13,'AMANDA SINTALA','1990-10-10','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(2,'FERNANDO SINTALA','1980-06-18','M','2003-02-03','D',2500);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(14,'LUANA PERRELA MARCELINO','2010-12-10','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(14,'LUCAS PERRELA MARCELINO','2022-11-01','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(14,'LAURA PERRELA MARCELINO','2014-03-03','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(14,'LANA PERRELA MARCELINO','2011-04-08','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(3,'Ana Sophia Araújo','1985-03-25','M','1999-05-11','C',2809);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(15,'Enzo Gabriel Cunha','2003-06-27','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(15,'Sarah Viana','2002-12-16','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'Lara Azevedo','1961-01-05','M','1993-03-10','C',13487);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(16,'Enzo Santos','2020-06-25','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'Matheus da Paz','1984-05-12','F','2008-07-17','C',2888);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(17,'Clarice Porto','2020-01-19','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(17,'Alexandre da Cruz','2023-10-03','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'Heloísa Freitas','1965-04-16','F','1997-04-29','S',14131);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(18,'Sr. Bryan Nascimento','2003-04-16','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(18,'Dr. Otávio Ferreira','2001-06-23','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(18,'Sra. Maria Alice Costa','2012-11-17','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(18,'Marcos Vinicius Gonçalves','2021-05-22','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'Isabelly da Mota','1983-12-22','F','1992-05-14','S',13838);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(19,'Rafael Dias','2009-11-05','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(19,'Enzo Castro','2012-12-07','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(19,'Lorenzo Moreira','2005-07-14','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'Dr. Emanuel Fogaça','1983-11-17','F','1992-06-06','V',4074);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(20,'Maysa da Cunha','2018-03-05','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(20,'Srta. Bruna Rezende','2012-11-28','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(20,'Pedro Miguel das Neves','2023-04-18','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(20,'Sr. Enzo Azevedo','2010-09-25','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'Emanuelly Campos','1967-03-07','F','2009-04-19','C',14355);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(21,'Sra. Clara Sales','2013-06-17','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(3,'Laís da Conceição','1969-01-04','M','1994-10-02','C',11444);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(22,'Vinicius Teixeira','2008-12-09','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(22,'Dra. Lara Nunes','2012-04-25','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(22,'Daniel Silva','2016-10-16','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'Vitor Gabriel Barros','1989-04-19','F','1993-09-24','S',7141);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(23,'Pedro Lucas da Cruz','2023-02-25','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(23,'Maria Vitória Campos','2013-02-02','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(3,'Maria Vitória Rezende','1978-01-01','F','1998-07-22','V',9828);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(24,'Alana Correia','2023-03-13','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(24,'Sophia Fogaça','2021-10-22','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(3,'Sr. Gustavo Pinto','1965-05-19','M','2005-06-09','S',13380);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(25,'Thiago Ferreira','2017-01-12','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'Luiz Fernando Cavalcanti','1989-08-14','F','2000-02-26','S',5077);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(26,'Lívia da Paz','2005-03-14','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(26,'Sr. Marcelo Souza','2000-01-08','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(26,'Giovanna Rodrigues','2000-08-30','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(26,'João Guilherme Lima','2008-02-23','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(3,'Erick Cardoso','1962-11-30','M','2006-07-15','S',2925);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(27,'Vitor Hugo Teixeira','2004-04-11','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(27,'Rafael Ribeiro','2018-09-15','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(27,'Francisco Souza','2020-08-21','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(27,'Clara Viana','2023-06-22','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'Theo Lima','1973-07-29','F','2002-09-15','S',13138);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(28,'Manuela Porto','2004-02-12','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(28,'Enzo Gabriel Campos','2011-07-03','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(28,'Nicolas Vieira','2007-10-30','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(28,'Clarice Almeida','2002-06-01','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'Dra. Ana Carolina Dias','1962-04-17','F','1991-01-26','S',14605);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(29,'Sr. Luiz Gustavo Duarte','2009-06-22','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(29,'Luiza da Rosa','2018-05-07','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(29,'Thiago Ribeiro','2008-04-07','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'Júlia da Mota','1963-03-18','F','1993-04-19','S',4666);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(30,'Larissa Moraes','2014-05-31','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(30,'Letícia Barros','2022-11-29','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(30,'Melissa Castro','2002-01-23','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(30,'Sabrina Mendes','2003-09-19','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'Diogo da Mota','1978-03-31','F','2005-04-07','S',13549);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(31,'Kevin da Mata','2009-06-23','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'Elisa Cardoso','1975-01-29','M','2008-09-22','D',12163);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(32,'Benjamin Viana','2000-07-02','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(32,'Vitor Gabriel Duarte','2005-08-28','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(32,'Luiza Rocha','2007-04-10','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(3,'Ana Carolina da Cunha','1972-11-22','F','1990-01-27','V',4227);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(33,'Emanuella Ramos','2009-09-14','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(33,'Pietra Rodrigues','2005-04-07','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(33,'Gustavo da Rosa','2001-12-27','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(33,'Sarah Viana','2002-01-27','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'Sra. Ana Carolina Barros','1979-11-16','F','2006-03-23','S',10717);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(34,'Marcela da Cruz','2001-12-07','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(34,'Ana Júlia da Mata','2002-05-01','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(34,'Ana Clara Duarte','2013-09-26','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'Miguel Farias','1979-09-12','F','2010-03-25','S',11237);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(35,'Pedro Henrique Cardoso','2014-04-06','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'Maria Luiza Silveira','1970-10-06','F','1998-11-15','D',2719);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(36,'Raul Lopes','2008-02-14','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(36,'João Vitor Costela','2022-11-08','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(36,'Fernanda Ramos','2010-10-04','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'André Ramos','1981-02-18','F','2009-02-26','S',11695);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(37,'Breno Teixeira','2007-04-02','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'Emanuella Costela','1971-11-16','F','1992-05-04','C',14861);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(38,'João Lucas Gomes','2005-05-14','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(38,'Maria Cecília Jesus','2020-10-23','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'Marcela Alves','1982-09-21','F','2008-11-14','S',6742);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(39,'Rafael Cavalcanti','2004-07-26','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(39,'Carlos Eduardo Cavalcanti','2018-10-28','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(39,'Gabriel Gomes','2020-07-30','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(39,'Theo Mendes','2006-12-05','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'Maysa Ferreira','1977-03-13','F','2006-08-16','V',9577);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(40,'Benjamin Carvalho','2021-07-31','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(40,'Emilly Barbosa','2000-02-14','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(40,'Sr. Pedro Miguel Ferreira','2005-07-01','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(40,'Sra. Maria Clara Pereira','2019-01-31','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'Carlos Eduardo Cardoso','1990-01-17','M','1995-01-27','V',2744);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(41,'Alícia Moura','2019-10-27','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(41,'Bianca Pinto','2004-05-02','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'Henrique Moreira','1990-08-03','F','1991-05-11','C',13997);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(42,'Sr. Rodrigo Farias','2022-09-10','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(42,'João Gabriel Oliveira','2021-02-12','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(5,'Srta. Eduarda da Cruz','1987-03-20','F','1996-01-10','V',3560);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(43,'Alice da Luz','2011-04-21','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(43,'Yasmin Farias','2009-01-28','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(2,'Yuri Cavalcanti','1973-01-06','F','1991-04-27','S',11234);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(44,'Clarice da Paz','2015-08-30','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(44,'Dr. Enzo das Neves','2000-10-21','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(44,'Caroline Nunes','2011-03-03','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(44,'Bernardo Freitas','2011-12-12','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'Maitê Nunes','1983-02-13','F','2008-03-30','C',3988);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(45,'Sr. Carlos Eduardo Ferreira','2006-01-28','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(45,'Emanuella Azevedo','2003-09-09','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(45,'Larissa Monteiro','2010-09-03','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'Maria Silva','1963-12-08','F','2003-02-09','C',13432);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(46,'Caroline Fernandes','2001-07-05','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(2,'Sra. Agatha Silveira','1987-06-10','F','2008-04-27','V',4190);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(47,'Rebeca da Paz','2012-05-23','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(47,'Ana Clara Melo','2021-03-15','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(2,'Sr. Thiago Jesus','1977-04-03','F','2000-07-10','S',9312);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(48,'Júlia Martins','2013-09-09','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(48,'Sra. Maria Clara Costela','2006-07-12','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(48,'Natália Nascimento','2023-01-17','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'Srta. Mariana Jesus','1973-10-25','F','2008-08-23','D',11416);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(49,'Heitor Gomes','2007-02-25','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(2,'Valentina Martins','1975-10-27','F','2005-01-12','C',14746);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(50,'Nicole da Rosa','2017-05-23','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(50,'Vitória da Cunha','2022-06-01','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'Gustavo Henrique Silva','1982-08-03','F','2001-05-28','D',5902);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(51,'Vitor Gabriel Duarte','2022-11-22','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(4,'Enzo Gabriel da Paz','1965-01-05','F','1990-10-31','D',2435);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(52,'Felipe Ribeiro','2020-10-18','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(52,'Lorenzo Peixoto','2021-06-05','F');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(52,'Caroline Nogueira','2016-10-26','F');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(2,'Elisa da Conceição','1982-04-28','M','1990-03-10','D',4936);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(53,'Yago Pereira','2007-06-12','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(53,'Samuel Silveira','2015-10-22','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(53,'Matheus Farias','2004-02-17','M');
insert into empregado(cod_depto, nome, dt_nascimento, sexo, dt_admissao, civil, salario) values(1,'Beatriz Rezende','1982-09-18','F','2008-01-27','V',3336);
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(54,'Maria Vitória Lopes','2015-01-22','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(54,'Rebeca Santos','2014-07-09','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(54,'Lavínia da Cruz','2016-02-25','M');
insert into dependente(cod_emp, nome, dt_nascimento, sexo) values(54,'Emanuella Farias','2021-09-11','M');
   ```

## Conteúdo do Repositório para Material Didático

Neste repositório, você encontrará uma série de aulas e exemplos práticos que cobrem os seguintes tópicos essenciais do MySQL:

### Tipos de Relacionamentos
- **Relacionamentos Um-para-Um (1:1)**
- **Relacionamentos Um-para-Muitos (1:N)**
- **Relacionamentos Muitos-para-Muitos (N:N)**

### Comandos JOIN
- **INNER JOIN**
- **LEFT JOIN**
- **RIGHT JOIN**
- **FULL JOIN**
- **SELF JOIN**

### VIEWS
- **Criação de Views**
- **Gerenciamento de Views**
- **Utilização de Views em Consultas**

### Tabelas Temporárias
- **Criação de Tabelas Temporárias**
- **Manipulação de Tabelas Temporárias**
- **Vantagens e Usos Comuns**

### Tuplas
- **Definição e Uso de Tuplas**
- **Inserção e Seleção de Tuplas**
- **Manipulação de Dados em Tuplas**

### Transactions
- **Início e Fim de Transações**
- **COMMIT e ROLLBACK**
- **Controle de Transações**

### Triggers
- **Criação de Triggers**
- **Tipos de Triggers (BEFORE, AFTER)**
- **Aplicações Práticas de Triggers**

### Procedures
- **Criação e Execução de Procedures**
- **Passagem de Parâmetros**
- **Exemplos de Procedures**

### Functions
- **Criação de Functions**
- **Diferenças entre Procedures e Functions**
- **Exemplos de Utilização de Functions**

## Objetivo

O objetivo deste repositório é proporcionar um material de estudo estruturado e fácil de seguir para aqueles que desejam aprender ou aprimorar suas habilidades em MySQL. Cada tópico é abordado com explicações teóricas acompanhadas de exemplos práticos que facilitam a compreensão e aplicação dos conceitos.

## Como Utilizar Este Repositório

1. **Clone o Repositório:**
   ```sh
   git clone https://github.com/seu-usuario/repo-aulas-mysql.git
   ```

2. **Navegue pelos Diretórios:**
   Cada tópico tem seu próprio diretório contendo scripts SQL, notas de aula e exemplos práticos.

3. **Siga as Instruções:**
   Leia as instruções e execute os scripts fornecidos em seu ambiente MySQL para praticar e experimentar os conceitos abordados.

4. **Pratique e Experimente:**
   Experimente modificar os exemplos e criar seus próprios scripts para reforçar seu entendimento dos tópicos.

## Contribuições

Contribuições são bem-vindas! Se você deseja adicionar novos tópicos, melhorar os existentes ou corrigir erros, sinta-se à vontade para abrir um pull request. Para sugestões e melhorias, você também pode abrir uma issue.

## Contato

Professor Victor Sena Icoma: victorsena3010@gmail.com
