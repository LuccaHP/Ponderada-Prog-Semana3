
### Schema do banco de dados em PostgreSQL (XML)
```sql
-- Criação da tabela Country
CREATE TABLE Country (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255),
    icon TEXT
);

-- Criação da tabela University
CREATE TABLE University (
    id SERIAL PRIMARY KEY,
    country_id INTEGER REFERENCES Country(id),
    name VARCHAR(255)
);

-- Criação da tabela User
CREATE TABLE User (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255),
    country_id INTEGER REFERENCES Country(id),
    email TEXT,
    birthday DATE,
    gender TEXT,
    university_id INTEGER REFERENCES University(id)
);

-- Criação da tabela Student
CREATE TABLE Student (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES User(id),
    country_pov TEXT,
    comportamental_type TEXT
);

-- Criação da tabela Tutor
CREATE TABLE Tutor (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES User(id)
);

-- Criação da tabela Group
CREATE TABLE Group (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255),
    tutor_id INTEGER REFERENCES Tutor(id)
);

-- Criação da tabela Team
CREATE TABLE Team (
    id SERIAL PRIMARY KEY,
    student_id INTEGER REFERENCES Student(id),
    group_id INTEGER REFERENCES Group(id)
);

-- Criação da tabela Board
CREATE TABLE Board (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES User(id),
    content TEXT,
    date DATE
);

-- Criação da tabela Feedback
CREATE TABLE Feedback (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES User(id),
    feedback_text TEXT,
    date DATE,
    destinatary_id INTEGER REFERENCES Student(id)
);
```

### Modelagem SQL
```sql
-- ---
-- Globals
-- ---

-- SET SQL_MODE="NO_AUTO_VALUE_ON_ZERO";
-- SET FOREIGN_KEY_CHECKS=0;

-- ---
-- Table 'User'
-- 
-- ---

DROP TABLE IF EXISTS `User`;
		
CREATE TABLE `User` (
  `id` INTEGER NULL AUTO_INCREMENT DEFAULT NULL,
  `name` VARCHAR NULL DEFAULT NULL,
  `country_id` INTEGER NULL DEFAULT NULL,
  `email` MEDIUMTEXT NULL DEFAULT NULL,
  `birthday` DATE NULL DEFAULT NULL,
  `gender` MEDIUMTEXT NULL DEFAULT NULL,
  `university_id` INTEGER NULL DEFAULT NULL,
  PRIMARY KEY (`id`)
);

-- ---
-- Table 'Country'
-- 
-- ---

DROP TABLE IF EXISTS `Country`;
		
CREATE TABLE `Country` (
  `id` INTEGER NULL AUTO_INCREMENT DEFAULT NULL,
  `name` VARCHAR NULL DEFAULT NULL,
  `icon` MEDIUMTEXT NULL DEFAULT NULL,
  PRIMARY KEY (`id`)
);

-- ---
-- Table 'University '
-- 
-- ---

DROP TABLE IF EXISTS `University `;
		
CREATE TABLE `University ` (
  `id` INTEGER NULL AUTO_INCREMENT DEFAULT NULL,
  `country_id` INTEGER NULL DEFAULT NULL,
  `name` VARCHAR NULL DEFAULT NULL,
  PRIMARY KEY (`id`)
);

-- ---
-- Table 'Student'
-- 
-- ---

DROP TABLE IF EXISTS `Student`;
		
CREATE TABLE `Student` (
  `id` INTEGER NULL AUTO_INCREMENT DEFAULT NULL,
  `user_id` INTEGER NULL DEFAULT NULL,
  `country_pov` MEDIUMTEXT NULL DEFAULT NULL,
  `comportamental_type` MEDIUMTEXT NULL DEFAULT NULL,
  PRIMARY KEY (`id`)
);

-- ---
-- Table 'Tutor'
-- 
-- ---

DROP TABLE IF EXISTS `Tutor`;
		
CREATE TABLE `Tutor` (
  `id` INTEGER NULL AUTO_INCREMENT DEFAULT NULL,
  `user_id` INTEGER NULL DEFAULT NULL,
  PRIMARY KEY (`id`)
);

-- ---
-- Table 'Group'
-- 
-- ---

DROP TABLE IF EXISTS `Group`;
		
CREATE TABLE `Group` (
  `id` INTEGER NULL AUTO_INCREMENT DEFAULT NULL,
  `name` VARCHAR NULL DEFAULT NULL,
  `tutor_id` INTEGER NULL DEFAULT NULL,
  PRIMARY KEY (`id`)
);

-- ---
-- Table 'Team'
-- 
-- ---

DROP TABLE IF EXISTS `Team`;
		
CREATE TABLE `Team` (
  `id` INTEGER NULL AUTO_INCREMENT DEFAULT NULL,
  `student_id` INTEGER NULL DEFAULT NULL,
  `group_id` INTEGER NULL DEFAULT NULL,
  PRIMARY KEY (`id`)
);

-- ---
-- Table 'Board'
-- 
-- ---

DROP TABLE IF EXISTS `Board`;
		
CREATE TABLE `Board` (
  `id` INTEGER NULL AUTO_INCREMENT DEFAULT NULL,
  `user_id` INTEGER NULL DEFAULT NULL,
  `content` MEDIUMTEXT NULL DEFAULT NULL,
  `date` DATE NULL DEFAULT NULL,
  PRIMARY KEY (`id`)
);

-- ---
-- Table 'Feedback'
-- 
-- ---

DROP TABLE IF EXISTS `Feedback`;
		
CREATE TABLE `Feedback` (
  `id` INTEGER NULL AUTO_INCREMENT DEFAULT NULL,
  `user_id` INTEGER NULL DEFAULT NULL,
  `feedback_text` MEDIUMTEXT NULL DEFAULT NULL,
  `date` DATE NULL DEFAULT NULL,
  `destinatary_id` INTEGER NULL DEFAULT NULL,
  PRIMARY KEY (`id`)
);

-- ---
-- Foreign Keys 
-- ---

ALTER TABLE `User` ADD FOREIGN KEY (country_id) REFERENCES `Country` (`id`);
ALTER TABLE `User` ADD FOREIGN KEY (university_id) REFERENCES `University ` (`id`);
ALTER TABLE `University ` ADD FOREIGN KEY (country_id) REFERENCES `Country` (`id`);
ALTER TABLE `Student` ADD FOREIGN KEY (user_id) REFERENCES `User` (`id`);
ALTER TABLE `Tutor` ADD FOREIGN KEY (user_id) REFERENCES `User` (`id`);
ALTER TABLE `Group` ADD FOREIGN KEY (tutor_id) REFERENCES `Tutor` (`id`);
ALTER TABLE `Team` ADD FOREIGN KEY (student_id) REFERENCES `Student` (`id`);
ALTER TABLE `Team` ADD FOREIGN KEY (group_id) REFERENCES `Group` (`id`);
ALTER TABLE `Board` ADD FOREIGN KEY (user_id) REFERENCES `User` (`id`);
ALTER TABLE `Feedback` ADD FOREIGN KEY (user_id) REFERENCES `User` (`id`);
ALTER TABLE `Feedback` ADD FOREIGN KEY (destinatary_id) REFERENCES `Student` (`id`);

-- ---
-- Table Properties
-- ---

-- ALTER TABLE `User` ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
-- ALTER TABLE `Country` ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
-- ALTER TABLE `University ` ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
-- ALTER TABLE `Student` ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
-- ALTER TABLE `Tutor` ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
-- ALTER TABLE `Group` ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
-- ALTER TABLE `Team` ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
-- ALTER TABLE `Board` ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
-- ALTER TABLE `Feedback` ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;

-- ---
-- Test Data
-- ---

-- INSERT INTO `User` (`id`,`name`,`country_id`,`email`,`birthday`,`gender`,`university_id`) VALUES
-- ('','','','','','','');
-- INSERT INTO `Country` (`id`,`name`,`icon`) VALUES
-- ('','','');
-- INSERT INTO `University ` (`id`,`country_id`,`name`) VALUES
-- ('','','');
-- INSERT INTO `Student` (`id`,`user_id`,`country_pov`,`comportamental_type`) VALUES
-- ('','','','');
-- INSERT INTO `Tutor` (`id`,`user_id`) VALUES
-- ('','');
-- INSERT INTO `Group` (`id`,`name`,`tutor_id`) VALUES
-- ('','','');
-- INSERT INTO `Team` (`id`,`student_id`,`group_id`) VALUES
-- ('','','');
-- INSERT INTO `Board` (`id`,`user_id`,`content`,`date`) VALUES
-- ('','','','');
-- INSERT INTO `Feedback` (`id`,`user_id`,`feedback_text`,`date`,`destinatary_id`) VALUES
-- ('','','','','');
```

# Documentação do Banco de Dados

## Visão Geral

Este banco de dados é projetado para gerenciar e armazenar informações referentes a um website que oferece suporte ao jogo de negócios Cesim, incluindo dados sobre usuários, países, universidades, estudantes, tutores, grupos, times, quadros de avisos e feedbacks. O esquema do banco de dados utiliza múltiplas tabelas inter-relacionadas para facilitar a organização e o acesso aos dados.

## Chaves Estrangeiras

As **chaves estrangeiras** são um conceito fundamental em bancos de dados relacionais. Elas são usadas para criar um vínculo entre duas tabelas, estabelecendo e impondo uma relação de interdependência entre os dados. Essas chaves garantem a integridade referencial do banco de dados, assegurando que relações entre registros de diferentes tabelas sejam mantidas corretamente.

### Funções das Chaves Estrangeiras no Esquema

- **Vínculo entre Usuário e País/Universidade**: A chave estrangeira em `User` que referencia `Country` e `University` assegura que cada usuário esteja vinculado a um país e uma universidade válidos, respectivamente.
- **Relacionamento entre Estudantes e Usuários**: A chave estrangeira em `Student` que referencia `User`, oferecendo o tipo Estudante para um usuário.
- **Relacionamento entre Tutores e Usuários**: Similarmente, cada tutor é conectado a um usuário através de uma chave estrangeira, oferecendo o tipo Tutor para um usuário.
- **Organização de Grupos por Tutores**: Em `Group`, a chave estrangeira que aponta para `Tutor` define a liderança de cada grupo, atribuindo um tutor responsável.
- **Composição de Times por Estudantes e Grupos**: As chaves em `Team` permitem que cada time seja composto por estudantes específicos e esteja vinculado a um grupo particular.
- **Publicações em Quadros de Avisos e Feedbacks**: Em `Board` e `Feedback`, as chaves que apontam para `User` e `Student` (no caso de Feedback) garantem que as publicações e feedbacks possam ser associados aos usuários e destinatários apropriados.

## Comportamento do Banco de Dados

O banco de dados é configurado para oferecer flexibilidade, integridade e uma estrutura clara para o gerenciamento de dados relacionados ao Cesim Game. As tabelas são projetadas para armazenar não apenas dados estáticos como nomes e detalhes de identificação, mas também informações dinâmicas, como feedbacks e publicações em quadros de avisos, que são essenciais para a operação diária do jogo.

### Integridade e Segurança

As opções de configuração e as chaves estrangeiras garantem que todas as inserções, atualizações e exclusões de dados sejam realizadas com a manutenção da integridade. Por exemplo, a remoção de um usuário automaticamente influencia a remoção de suas informações associadas em outras tabelas, como estudante, tutor, publicações e feedbacks.

### Flexibilidade e Escalabilidade

A estrutura permite fácil expansão e modificação. Novas relações ou tabelas podem ser adicionadas conforme necessário sem interrupções significativas. As chaves estrangeiras e as opções de configuração, como tipos de dados e permissões de nulidade, podem ser ajustadas para refletir mudanças nas necessidades organizacionais.

## Conclusão

O banco de dados descrito neste documento é uma ferramenta robusta e adaptável para a gestão de informações do jogo. Ele foi projetado para ser seguro, eficiente e fácil de modificar, com uma forte ênfase na integridade e na relevância dos dados.
