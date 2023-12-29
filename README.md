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

