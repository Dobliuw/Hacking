![[Pasted image 20230215165210.png]]

--- 

### MODELO ER (Con Notación de Chen ):  

###### El diagrama de chen es una manera de representar los datos: 

- ### Entidad: 
#### La entidad es un algo en el sistema, por ejemplo, ordenes de compra, etc., clientes, es decir, diversas entidades que existe, algo asi como un objeto.
###### Las mismas se representan de la sig. manera: 

![[Pasted image 20230403162341.png]]

- ### Atributos: 
#### El atributo es un valor que compone a la entidad.
##### Los mismos se representan de la sig. manera: 
### Simples:
![[Pasted image 20230403162759.png]]
#### Ahora bien, estos atributos pueden ser siemples como se grafica en el ejemplo de arriba, o pueden ser compuestos, es decir, que el atributo se componga de atributos. O tambien pueden ser altributos multivalor. 

### Compuestos: 
##### Es decir se componene de atributos.
![[Pasted image 20230403163235.png]]

### Multivalor: 
#### Atributos con más de un valor.
![[Pasted image 20230403163410.png]]

### Derivados:
##### Atributos que deriban y se obtienen a partir de otros atributos, por ejemplo, la antiguedad de una casa de podria obtener a partir del atributo "Fecha de creación".
![[Pasted image 20230403163806.png]]

### KEY:
#####  "Propiedad" unica que contiene el atributo para volverlo unico como un id, un documento, mail, etc. 
![[Pasted image 20230403164237.png]]

### Registros: 
#### Estos son los valores en conjuntos insertados en la tabla, por ejemplo, en una tabla (Entidad) de "usuarios" el ingreso del usuario "Owen" con diversos valores, seria un registro.

--- 

# Manipulación de base de datos, tablas y columnas: 
## Mariadb con mysql para los ejemplos.

### CREACIÓN de base de datos: 
```sql
create database "usersdb";
```

### USO de la base de  datos:
```sql
use "usersdb";
```

### CREACIÓN de TABLA para la base de datos: 
```sql
create table "users"(
	user_id int primary key auto_increment,
	name varchar(50) not null,
	email varchar(50) not null,
	password varchar(50) not null
);
```

### INSERTAR VALORES en las tablas:
```sql
insert into "users"(name, email, password)
values("Name1", "email1@gmail.com", "password1"), ("Name2", "email2@gmail.com", "password2")
```

### FOREING KEY: 

### CREANDO una tabla para agregar la FK:
```sql
create table "orders"(
	order_id int primary key auto_increment,
	profesional varchar(50) not null,
	orderDate date not null, 
	user_id int not null,
	constraint user_id foreing key (user_id)
	references usersdb(user_id)
);
```
##### De esta manera creamos una nueva tabla con el nombre de "orders" en donde tendremos varios campos, pero al final,  declaramos un campo "user_id" para posteriormente volverlo una FOREING KEY la cual esta referenceada a otra tabla y otro campo (En este caso "usersdb"  y "user_id")

---

### #ACLARACION 

### La query "ALTER TABLE {table_name}"  sirve para ALTERar una TABLA

---

### MODIFICANDO una tabla para agregar la FK: 
```sql
alter table "orders"
add constrain user_id
foreing key (user_id) references usersdb(user_id);

-- Otra manera:

alter table "orders"
add foreing key (user_id) references usersdb(user_id);

```

### ELIMINANDO una FK: 
```sql
alter table "orders"
drop foreing key user_id;
```


## Diagrama de la relación: 

![[Pasted image 20230404130357.png]]

### ELIMINAR un registro especifico: 
```sql
delete from users where user_id=7
```

### MODIFICAR un registro: 
```sql
-- Edit: 

update users set name='NuevoNombre' where name='Ejemplo'

-- Multiple edit:

update users 
set name='NuevoNombre',
email='NuevoEmail'
where name='Ejemplo'
```

### DISCRIMAR datos: 
```sql
select * from users where not name='Dobliuw'
-- Traer todos los registros de la tabla users menos cuando name = 'Dobliuw'
```
---

# Consultas de datos: 

### Consultar TABLAS (DB en uso): 
```sql
show tables; 
```

### Consultar las COLUMNAS de una tabla (DB en uso):
```sql
show columns from "users";
```

### Consultar BASES DE DATOS registradas: 
```sql
select schema_name from information_schema.schemata;
```

### Consultar TABLAS de una db: 
```sql
select table_name from information_schema.tables where table_schema='usersdb';
```

### Consultar COLUMNAS de una tabla de una db: 
```sql
select column_name from information_schema.columns where table_schema='usersdb' and table_name='users';
```

### Consulta de una TABLA uniendo FK a la query:
```sql
select * from orders join users where users.user_id=orders.user_id;  
```

### Consulta de datos con AS y operaciones:
```sql
select number,number*2 as numberDoble from orders;
```

### ORDENAR la consulta: 
```sql
select * from orders order by number 
-- Seleccionar todo de la tabla orders ordenado por numbers de manera ascendente

select * from orders order by number DESC
-- Seleccionar todo de la tabla orders ordenado por numbers de manera descendente 

```

### Consultar IGNORANDO REPETIDOS:
```sql
select distinct * from  users
```
---

# Ejecutar archivos .sql: 

- ###   Para MySQL: 
```shell
mysql -u usuario -p < archivo.sql
```

- ### Para PostgreSQL: 
```shell
psql -U usuario -f archivo.sql
```

- ### Para SQL Server: 
```shell
sqlcmd -S servidor -U usuario -P contraseña -i archivo.sql
```

- ### Para Oracle: 
```shell
sqlplus usuario/contraseña@nombre_instancia @archivo.sql
```
