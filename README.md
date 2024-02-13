# MySQL Cheat Sheet

## Comandos básicos de MySQL

### Login

    $ mysql -u root -p

### Mostrar usuarios

    $ SELECT User, Host FROM mysql.user;

### Crear usuario

    $ CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';

### Otorgar todos los privilegios a todas las bases de datos

    $ GRANT ALL PRIVILEGES ON * . * TO 'usernma'@'localhost';
    $ FLUSH PRIVILEGES;

### Mostrar privilegios

    $ SHOW GRANTS FOR 'username'@'localhost';

### Remover privilegios

    $ REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'username'@'localhost';

### Eliminar un usuario

    $ DROP USER 'username'@'localhost';

### Salir

    $ exit;

## Conceptos básicos de SQL

### Mostrar las bases de datos

    SHOW DATABASES;

### Crear una base de datos

    CREATE DATABASE acme;

### Eliminar una base de datos

    DROP DATABASE acme;

### Seleccionar una base de datos

    USE acme;

### Crear una tabla

    CREATE TABLE users(
        id INT AUTO_INCREMENT,
        first_name VARCHAR(100),
        last_name VARCHAR(100),
        email VARCHAR(50),
        password VARCHAR(100),
        is_admin BOOLEAN,
        register_data DATETIME,
        PRIMARY KEY(id)
    );

### Eliminar una tabla

    DROP TABLE users;

### Mostrar las tablas

    SHOW TABLES;

### Insertar un registro en una tabla

    INSERT INTO users (first_name, last_name, email, password, is_admin, register_data)
    VALUES ('Martin', 'Wilches', 'martinwilchesp@gmail.com', 'abcd1234', 1, now());

### Consultar registros de una tabla

    SELECT * FROM users;
    SELECT first_name FROM users;

### Clausula WHERE

    SELECT * FROM users WHERE location = 'New York';
    SELECT * FROM users WHERE location != 'Boston' AND is_admin = 1;

### Eliminar una registro

    DELETE FROM users WHERE id = 1;

### Actualizar un registro

    UPDATE users SET is_admin = 0 WHERE ID = 100;

### Añadir una nueva columna a una tabla

    ALTER TABLE users ADD age VARCHAR(3);

### Modificar una columna

    ALTER TABLE users MODIFY COLUMN age INT;

### Ordenar registros consultados

    SELECT * FROM users ORDER BY age DESC;

### Concatenar columnas

    SELECT (first_name, '', last_name) AS name, age FROM users;

### Seleccionar registros unicos

    SELECT DISTINCT name FROM users;

### Seleccionar registros dentro de un rango

    SELECT * FROM users WHERE age BETWEEN 20 AND 25;

### Seleccionar registros a traves de coincidencias parciales en el campo especificado

    SELECT * FROM users WHERE dept LIKE 'd%';
    SELECT * FROM users WHERE dept LIKE 'dev%';
    SELECT * FROM users WHERE dept LIKE '%t';
    SELECT * FROM users WHERE dept LIKE 't%';
    SELECT * FROM users WHERE dept LIKE '%tmp%';

### Seleccionar los registros que no coincidan de forma parcial con el campo especificado

    SELECT * FROM users WHERE last_name NOT LIKE 'a%';

### Seleccionar los registros que se encuentren en un conjunto de datos en un campo especifico

    SELECT * FROM users WHERE dept IN ('design', 'sales');

### Crear un indice

    CREATE INDEX LIndex ON users(location);

### Eliminar un indice

    DROP INDEX LIndex ON users;

### Crear una tabla que contenga llaves foraneas

    CREATE TABLE posts(
        id INT AUTO_INCREMENT,
        user_id INT,
        body VARCHAR(20),
        PRIMARY KEY(id),
        FOREIGN KEY (user_id) REFERENCES users(id)
    );

## Multiples tablas

### INNER JOIN - En el resultado de la consulta se agregan todos los registros de ambas tablas, incluso los que no cumplen con la condición especificada

    SELECT
        u.first_name,
        u.age,
        p.body
    FROM users AS 'u'
    INNER JOIN posts AS 'p'
    ON u.id = p.user_id
    ORDER BY p.id;

### LEFT JOIN - En el resultado de la consulta se agregan todos los registros de la tabla de la izquierda (users <-> posts) que cumplan con la condición especificada

    SELECT
        u.first_name,
        p.body
    FROM users AS 'u'
    LEFT JOIN posts AS 'p'
    ON u.id = p.user_id;

### Funciones agregadas

    SELECT COUNT(id) FROM users;
    SELECT MAX(age) FROM users;
    SELECT MIN(age) FROM users;
    SELECT SUM(age) FROM users;
    SELECT UCASE(first_name), LCASE(last_name) FROM users;

### Agrupar filas que tengan el mismo valor en una o mas columnas especificas, siendo especialmente útil cuando se usan funciones agregadas.

    SELECT age, COUNT(age) FROM users group by age;
    SELECT age, COUNT(age) FROM users WHERE age > 20 GROUP BY age;
    SELECT age, COUNT(age) FROM users GROUP BY age HAVING COUNT(age) >= 2;