''![[Pasted image 20230215165210.png]]

---

```SQL
-- Creating an user after download myqsl
sudo mysql

CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'new_user'@'localhost';
FLUSH PRIVILEGES;

  
-- listar y ver la contrucción de una db:
select * from information_schema.columns where table_name='table_name';
 
-- Crear base de datos:
create database {name};

-- Eliminar base de datos: 
drop database {name}; 

-- Eliminar tabla:
drop table {name};

-- listar base de datos:
show databases;

-- conectarse a una base de datos:
use database | connect database

-- listar tablas de una base de datos:
show tables;

-- crear una tabla en la db:
create table users(
	userid int not null primary key auto_increment,
	username varchar (50) not null,
	password varchar (50) not null,
);

-- Add:
inser into users(username, password, email)
values ("owen", "123", "a@gmail.com"), ("masdatos", "para ingresar", "de manera multiple");

-- Foreing key 
alter table {table_name} add column {column_name} {...values}; 
alter table {table_name} add constrain {column_name} foreing key (column_name) references {table_name}({column}); 



```
