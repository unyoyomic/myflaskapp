# myflaskapp

USE myflaskapp;

CREATE USER 'Raluca'@'localhost' IDENTIFIED BY 'stf01dnd';

GRANT ALL PRIVILEGES ON myflaskapp.* TO 'Raluca'@'localhost';

GRANT SELECT, INSERT, DELETE ON myflaskapp.* TO 'Raluca'@'localhost';

FLUSH PRIVILEGES;

CREATE TABLE articles(id INT(11) AUTO_INCREMENT PRIMARY KEY, title varchar(255), author varchar(100), body text, register_date timestamp default current_timestamp);

CREATE TABLE users(id INT(11) AUTO_INCREMENT PRIMARY KEY, name varchar(100), 
email varchar(100), username varchar(30), password varchar(100), register_date timestamp default current_timestamp);


CREATE TABLE teams(team_id INT(11) AUTO_INCREMENT PRIMARY KEY, name varchar(255));

CREATE TABLE answer_types(answer_type_id INT(11) AUTO_INCREMENT PRIMARY KEY, type_name varchar(20));

CREATE TABLE agents(agent_id INT(11) AUTO_INCREMENT PRIMARY KEY, agent_name varchar(100));

CREATE TABLE question_difficulties(question_difficulty_id INT(11) AUTO_INCREMENT PRIMARY KEY, difficulty_name varchar(100));

CREATE TABLE quizzes(quizz_id INT(11) AUTO_INCREMENT PRIMARY KEY, name varchar(255), team_id INT(11),
FOREIGN KEY (team_id) REFERENCES teams(team_id));

CREATE TABLE questions(question_id INT(11) AUTO_INCREMENT PRIMARY KEY, question varchar(255), quizz_id INT(11), answer_type_id INT(11), question_difficulty_id INT(11),
FOREIGN KEY (quizz_id) REFERENCES quizzes(quizz_id), FOREIGN KEY (answer_type_id) REFERENCES answer_types(answer_type_id), 
FOREIGN KEY (question_difficulty_id) REFERENCES question_difficulties(question_difficulty_id));

CREATE TABLE answers(answer_id INT(11) AUTO_INCREMENT PRIMARY KEY, answer varchar(255), question_id INT(11) ,
FOREIGN KEY (question_id) REFERENCES questions(question_id));

CREATE TABLE agents_answers_by_questions(agent_id INT(11), FOREIGN KEY (agent_id) REFERENCES agents(agent_id), question_id INT(11), answer_id INT(11),
FOREIGN KEY (question_id) REFERENCES questions(question_id), FOREIGN KEY (answer_id) REFERENCES answers(answer_id));

CREATE TABLE quizzes_results(agent_id INT(11), FOREIGN KEY (agent_id) REFERENCES agents(agent_id), isPassed bool);

ALTER TABLE agents_answers_by_questions
ADD answer_id INT(11);

ALTER TABLE agents_answers_by_questions
ADD FOREIGN KEY (answer_id) REFERENCES answers(answer_id);

INSERT INTO teams (name)
VALUES ("TeamTest");

INSERT INTO quizzes (name, team_id)
VALUES ("QuizTest", 1);

INSERT INTO answer_types (type_name)
VALUES ("SingleAnswer");

INSERT INTO question_difficulties (difficulty_name)
VALUES ("Easy");

INSERT INTO questions (question,quizz_id, answer_type_id, question_difficulty_id)
VALUES ("Care este capitala Romaniei?", 1, 1, 1);

INSERT INTO questions (question,quizz_id, answer_type_id, question_difficulty_id)
VALUES ("Cine este cea mai iubita pisica de pe Pamant?", 1, 1, 1);

INSERT INTO questions (question,quizz_id, answer_type_id, question_difficulty_id)
VALUES ("Pe ce data este Anul Nou?", 1, 1, 1);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("Bucuresti",
1);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("Budapesta",
1);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("Bucegi",
1);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("Romania e un oras",
1);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("Peach",
2);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("Ppeeaacchh",
2);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("Peachy",
2);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("Peach <3",
2);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("31.dec",
3);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("de anul nou",
3);

INSERT INTO `myflaskapp`.`answers`
(`answer`,
`question_id`)
VALUES
("ce este Anul Nou?",
3);
