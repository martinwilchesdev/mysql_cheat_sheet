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