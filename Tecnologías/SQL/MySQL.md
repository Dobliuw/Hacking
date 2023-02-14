```SQL
-- Creating an user after download myqsl
sudo mysql

CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'new_user'@'localhost';
FLUSH PRIVILEGES;

  
-- listar y ver la contrucción de una db:
select * from information_schema.columns where table_name='table_name';
 
-- Crear base de datos:
create database name;

-- listar base de datos:
show databases;

-- conectarse a una base de datos:
use database | connect database

-- listar tablas de una base de datos:
show tables;

-- crear una tabla en la db:
create table users(
	userid int primary key,
	username varchar (50) not null,
	password varchar (50) not null,
);

-- Add:
inser into users(username, password, email)
values ("owen", "123", "a@gmail.com");
```
