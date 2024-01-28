# ✩ Lista 02: SQL ✩
## Resolva as questões utilizando as tabelas abaixo como referência:

```shell
+----+--------------+
| tabela_pessoa     |
+----+--------------+
| id | nome         |
+----+--------------+
|  1 | John Doe     |
|  2 | Jane Doe     |
|  3 | Alice Jones  |
|  4 | Bobby Louis  |
|  5 | Lisa Romero  |
+----+--------------+
+----+----------------+-----------+
| tabela_evento                   |
+----+----------------+-----------+
| id | evento         | pessoa_id |
+----+----------------+-----------+
|  1 | Evento A       |  2        |
|  2 | Evento B       |  3        |
|  3 | Evento C       |  2        |
|  4 | Evento D       |  NULL     |
+----+----------------+-----------+
```

### 01) Crie uma query para selecionar todas as pessoas 'tabela_pessoa' e os respectivos eventos 'tabela_evento' o qual elas participam.
````sql
SELECT p.id, p.nome, e.evento
FROM tabela_pessoa p
LEFT JOIN tabela_evento e ON p.id = e.pessoa_id;
````

### 02) Crie uma query para selecionar todas as pessoas 'tabela_pessoa' com sobrenome 'Doe'.
````sql
SELECT * FROM tabela_pessoa
WHERE nome LIKE '%Doe';
````

### 03) Crie uma query para adicionar um novo evento 'tabela_evento' e relacionar à pessoa 'Lisa Romero'.
````sql
SELECT id FROM tabela_pessoa WHERE nome = 'Lisa Romero';
INSERT INTO tabela_evento (evento, pessoa_id)
VALUES ('Evento novo', 5);
````

### 04) Crie uma query para atualizar 'Evento D' na 'tabela_evento' e relacionar à pessoa 'Joh Doe'.
````sql
SELECT id FROM tabela_pessoa WHERE nome = 'John Doe';
UPDATE tabela_evento
SET pessoa_id = 1
WHERE evento = 'Evento D';
````

### 05) Crie uma query para remover o 'Evento B' na 'tabela_evento'.
````sql
DELETE FROM tabela_evento
WHERE evento = 'Evento B';
````

### 06) Crie uma query para remover todas as pessoas 'tabela_pessoa' que não possuem eventos 'tabela_evento' relacionados.
````sql
DELETE FROM tabela_pessoa
WHERE id NOT IN (SELECT pessoa_id FROM tabela_evento);
````

### 07) Crie uma query para alterar a tabela 'tabela_pessoa' e adicionar a coluna 'idade' (int).
````sql
ALTER TABLE tabela_pessoa
ADD idade INT;
````

### 08) Crie uma query para criar uma tabela chamada 'tabela_telefone' que pertence a uma pessoa com seguintes campos:
````shell
    id: int (PK)
    telefone: varchar(200)
    pessoa_id: int(FK)
````

````sql
CREATE TABLE tabela_telefone (
    id INT PRIMARY KEY,
    telefone VARCHAR(200),
    pessoa_id INT,
    FOREIGN KEY (pessoa_id) REFERENCES tabela_pessoa(id)
);
````

### 09) Crie uma query para criar uma índice do tipo **único** na coluna telefone da 'tabela_telefone'.
````sql
CREATE UNIQUE INDEX id_ui_telefone
ON tabela_telefone (telefone);
````

### 10) Crie uma query para remover a 'tabela_telefone'.
````sql
DROP TABLE tabela_telefone;
````
