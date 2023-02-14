```SQL
-- Crear base de datos:
create database name;

-- listar base de datos:
\l

-- conectarse a una base de datos:
\c name

-- listar tablas de una base de datos:
\d

-- crear una tabla en la db:
create table users(
	userid int primary key,
	username varchar (50) not null,
	password varchar (50) not null,
);

create table roles(
	roleid int primary key,
	rolename varchar(50) unique not null
);

-- Relaciones:
create table users_roles(
	userid int not null,
	roleid int not null,
	primary key(userid, roleid),
	foreign key (roleid)
	references roles (roleid),
	foreign key (userid)
	references users (userid)
);

-- Add:
inser into users(username, password, email)
values ("owen", "123", "a@gmail.com");
```