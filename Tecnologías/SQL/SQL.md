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

### Agregando un nuevo campo:
```sql
-- Con esto podemos agregar una columna con los datos deseados y especificar despues de que columna agregarlo

alter table orders 
add column 'random' varchar(50) after user_id
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

###  Consulta DISCRIMINANDO datos: 
```sql
select * from users where not name='Dobliuw'
-- Traer todos los registros de la tabla users menos cuando name = 'Dobliuw'
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

### Consultar LIMITANDO los resultados:
```sql
-- Limitando la respuesta en 5 registros
select * from users limit 5 

-- Limitando la respuesta a 5 a partir del registro 3
select * from users limit 3,5
```

### Consultar con resultados RANDOM:
```sql
-- Esta query constantemente arrojaria dos registros aleatorios 
select * from users order by rand() limit 2 
-- (Podrian ingresarse condiciones)
```

### Consultar valores ENTRE un rango: 
```sql
select * from users where user_id between 4 and 10

-- Tambien es usado para las fechas: 

select * from {db} where dates between 'yyyy-mm-dd' and 'yyyy-mm-dd'
```

### Consultar valores con "REGEX" ( LIKE ):
```sql
-- Que empieze con 'D'
select * from users where name like 'D%'

-- Que termine con 'w'
select * from users where name like '%w'

-- Que tenga 'obli' en el texto
select * from users where name like '%obli%'

-- Que una 'b' en la tercera posición
select * from users where name like '__b%'

-- Que terminen con 'b' 
select * from users where name like '%_u_'

-- Que empieze con 'D' y termine con 'D'
select * from users where name like 'D%w'

-- Que sea un registro de 7 caracteres y la segunda posición tenga un 'o'
select * from users where name like '_o_____'
```

### Consultar valores con NULL y NOT NULL:
```sql
-- Seleccionar todos los que sean nulos 
select * from users where name is null order by ASC 

-- Seleccinoar todos los que no sean nulos 
select * from uesrs where name is not null order by ASC

```

### Consultar valores con IN: 
```sql
-- Seleccionar todos los registros que tengan un valor de user_id que este dentro de la tupla del in (3,4,5,6)
select * from users where user_id in (3,4,5,6)

select * from users where name in ("Dobliuw")

-- Seleccionar todos los registros que tenguna un valor de user_id que NO este dentro de la tupla del in (3,4,5,6)
select * from users where user_id not in (3,4,5,6)

```

---

# Subconsultas:  

###  Funciónes de AGREGACIÓN: 
```sql
-- ### IMPORTANTE ### -- 
-- Las funciones de agregación retornan un resultado, es decir, por ejemplo, ROUND(AVG(user_id)), devuelve el redondeamiento del promedio de los user_id, ese resultado puede ser renombrado con "as", por ejemplo "ROUND(AVG(user_id)) as result" ahora, result va a   ser el resultado y es importante recordar que este ressultado...
--  ########### NO SE PUEDE USAR EN OTRA FUNCIÓN DE AGREGACIÓN. ##############

-- Devuelve la cantidad de registros que tienn user_id
select COUNT(user_id) from users

-- Devuelve la suma de todos los user_id
select SUM(user_id) from users

-- Devuelve el promedio de los user_id
select AVG(user_id) from users

-- Devuelve un nro redondeado a 3 decimales del promedio de los user_id
select ROUND(AVG(user_id),3) from users

-- Devuelve el nombre como 'Nombre' y el valor MINIMO de user_id como 'ID' siempre y cuando name no sea NULL 
select name as 'Nombre', MIN(user_id) as 'ID' from users where name is not null 

-- Devuelve el nombre como 'Nombre' y el valor MAXIMO de user_id como 'ID' siempre y cuando name no sea NULL 
select name as 'Nombre', MAX(user_id) as 'ID' from users where name is not null
```

### Consultas con GROUP BY y HAVING:
```sql
-- El GROUP BY se utiliza para agrupar registros
select name as 'Nombre', ROUND(user_id / 2,2) as 'ID' from users group by user_id

-- El HAVING se usa como un where pero del resultado de una función
select name as 'Nombre', ROUND(user_id / 2,2) as 'ID' from users group by email having ID > 2;

-- Ejemplos: 
select distinct CategoryID as 'ID', ROUND(UnitPrice/2, 3) as 'Precio' from Products 
group by ID 
having Precio >= 10 
limit 0,20;
```

### ESTRUCTURA de una query: 
```sql
SELECT....FROM....
WHERE.....
GROUP BY....
HAVING....
ORDER BY....
LIMIT....
```

### Sub Consultas: 
```sql
-- Teniendo en cuenta que el select selecciona COLUMNAS, podriamos realizar una query (Subconsulta) la cual devuelva una columna

-- De esta manera estariamos trayendo 3 datos de la tabla users, pero agregando una columna con el apartado de number perteneciente a la tabla orders
SELECT name, email, password, (select number from orders) from users; 

-- Si bien para casos como el sig se utiliza el join, si la tabla orders tiene una FK asociada con la tabla users, podriamos solicitar que se unan esos datos junto a los usuarios: 
SELECT name as 'Nombre', 
email as 'Correo Electronico', 
password as 'Contraseña', 
(SELECT number from orders where users.user_id=orders.user_id) as 'Ordenes N°',
(SELECT date from orders where users.user_id=orders.user_id) as 'Fecha' from users
-- Ahora, esta query con 2 subconsultas dentro de ellas, devolveria una tabla como la sig: 
/*
+----------+------------------------+-------------------------------+---------+--------------
| Nombre   | Correo Electronico     | Contraseña                    | Ordenes N° | Fecha  
+----------+------------------------+-------------------------------+---------+--------------
| Dobliuw  | dobliuw@dobliuw.com    | U2!+BF!.hZy1ST4r1&6*&3Uu1&3mI |      11    | 1980-06-11     |
| ZaikoARG | zaikoarg@zaikoarg.com  | Z41k0+!1&dDxD_                |    NULL    | NULL           | 
| Valen    | valenmachu@gmail.com   | 1254821158644468              |    NULL    | NULL           |
| Brian    | brian@gmail.com        | Tomi2008                      |    NULL    | NULL           |
| Jose     | jose32@gmail.com       | jose32                        |       5    | 2012-12-12     |
| Roberto  | robertoperez@gmail.com | roberto1980                   |    NULL    | NULL           |
| David    | david@gmail.com        | mihijoelmejor                 |    NULL    | NULL           |
+----------+------------------------+-------------------------------+---------+--------------

Ahora, si no quisieramos los que tenga valor NULL, como aprendimos antes podriamos empezar a utilizar y mezclar conceptos
*/
SELECT name AS 'Nombre',  
email AS 'Correo Electronico',  
password AS 'Contraseña',  
(SELECT number FROM orders AS o WHERE u.user_id=o.user_id) AS Ordenes, 
(SELECT date FROM orders AS o WHERE u.user_id=o.user_id) AS Fecha 
FROM users AS u 
HAVING Fecha AND Ordenes IS NOT NULL;

-- Ejemplo: 
SELECT user_id as 'ID', 
name as 'Nombre',  
email as 'Correo Electronico',  
password as 'Contraseña',  
(SELECT number from orders as o where u.user_id=o.user_id) as Ordenes, 
(SELECT date from orders as o where u.user_id=o.user_id) as Fecha, 
( select group_concat('[!] ',u.user_id,' x ',number,' = ',u.user_id * number) from orders as o where u.user_id=o.user_id) as 'ID * Número' 
from users as u 
having Ordenes and Fecha is not null;

-- Resultado: 
/*
+----+---------+---------------------+-------------------------------+---------+------------
| ID | Nombre  | Correo              | Contraseña  | Ordenes |   Fecha    |    ID * Número  | 
+----+---------+---------------------+-------------------------------+---------+------------
|  1 | Dobliuw | dobliuw@dobliuw.com | U2!+BF!...  |      11 | 1980-06-11 | [!] 1 x 11 = 11 |
|  5 | Jose    | jose32@gmail.com    | jose32      |       5 | 2012-12-12 | [!] 5 x 5 = 25  |
+----+---------+---------------------+-------------------------------+---------+------------
*/

-- Tambien se puede usar para condiciones: 
select name as Nombre, email as Correo from users where (select number from orders where users.user_id=orders.user_id) is not null;

```

### Consultas con JOIN: 

- ### Cross JOIN: 
##### Sirve para unir tablas generando un nueva uniendo cada registro de manera multiplicada con los registros de la otra tabla, es decir, que si tengo una tabla de 3 registros y hago un cross join con otra tabla de 3 registros, voy a obtener una tabla con 9 registros, ya que estos se unen generando cada una de las posiblidades de union.

#### Hay que tener en cuenta que el cross join puede darse de manera implicita o explicita. Esto devuelve algo llamada 'PRODUCTO CARTESIANO'

#### IMPLICITA:
```sql
-- De esta manera estamos uniendo la tabla users y orders contemplando cada una de las posiblidades de union de la misma.
SELECT * FROM users, orders
```
#### EXPLICITA:
```sql
-- Lo mismo pero de manera explicita
SELECT * FROM users CROSS JOIN orders
```

![[Pasted image 20230406111340.png]]

- ### Inner JOIN: 
##### Se utiliza para fusionar tablas con valores que nos interesan, supongamos que tenemos una tabla de ESTUDIANTES y otra de TRABAJADORES, podriamos utilizar el INNER JOIN para muchos casos como, devolver las tablas fusionadas con los usuarios que trabajan y si estudian que estudian, solo aquellos que estudian y trabajan, etc.

#### Tambien hay que tener en cuenta en este otro caso que se puede hacer de manera explicita e implicita, pero siempre realizarla de manera explicita va a ser una mejor practica.


#### IMPLICITA:
```sql
-- De esta manera estamos uniendo la tabla users y orders contemplando cada una de las posiblidades de union de la misma.
SELECT * FROM users, orders WHERE users.user_id=orders.user_id
```
#### EXPLICITA:
```sql
-- Lo mismo pero de manera explicita 
SELECT * FROM users INNER JOIN orders ON users.user_id=orders.user_id
-- Tambien se suele usar solo el JOIN para hacer referencia a INNER JOIN 
```


### Ejemplo: 
```sql 
-- ON es como el WHERE pero cuando se usa INNER JOIN
SELECT * FROM tabla1 
INNER JOIN tabla2 
ON tabla1.nombre=tabla2.nombre
```
![[Pasted image 20230406112807.png]]

### Ejemplo: 
```sql 
-- ON es como el WHERE pero cuando se usa INNER JOIN
SELECT * FROM tabla1 
INNER JOIN tabla2 
ON tabla1.nombre=tabla2.nombre and tabla1.trabajo is not null and tabla2.estudio is not null
```

![[Pasted image 20230406112516.png]]

- ### Left JOIN: 
##### A diferencia de los otros joins, ese lo que tiene es que devuelve toda una tabla (La A) junto a los datos de la otra (La B), remplazando con  NULL los campos de los que no tenga datos. 

#### Ejemplo:
```sql
SELECT * FROM tabla1 LEFT JOIN tabla2 ON tabla1.nombre=tabla2.nombre
```

![[Pasted image 20230406153509.png]]

- ### Right join: 
##### A diferencia de los otros joins, ese lo que tiene es que devuelve toda una tabla (La B) junto a los datos de la otra (La A), remplazando con  NULL los campos de los que no tenga datos. 

#### Ejemplo:
```sql
SELECT * FROM tabla1 RIGHT JOIN tabla2 ON tabla1.nombre=tabla2.nombre
```

![[Pasted image 20230406154836.png]]

- ### Full JOIN: 
##### A diferencia del cross join, que devuelve todo "multiplicado", mientras que el full, trae todo de las dos tablas. ( Se simula con UNION )

## UNION y UNION ALL: 

- ### UNION: 

###### Este sirve para unir dos consultas (Siempre en lo posible que contengan los mismo datos) y elimina duplicados.

![[Pasted image 20230407170142.png]]

- ### UNION ALL:

###### Este sirve para unir dos cunsultas (Tambien en lo posible siempre deberian ser de los mismos datos) con la diferencia de que no elimina duplicados.

![[Pasted image 20230407165626.png]]

## Cardinalidad: 

- ### 1 a 1 (Uno a uno):

##### Consiste en una realción de un registro de una tabla con un registro de otra tabla, por ejemplo:  Una persona (En la tabla personas) se relaciona con un DNI (En la tabla de DNIS), un DNI pertenece a una persona, y una persona tiene un DNI.

- ### N a  1 (Muchos a uno):

##### Consiste en una relación de varios registros de una tabla con un registro de otra tabla. Por ejemplo:  Los libros (En la tabla lirbos ) se relacionan con un Autor (En la tabla atuores), un libro tiene un autor y un autor muchos libros.

- ### N a M (Muchos a muchos):  

##### Consiste en una relación de varios registros de una tabla con varios registros de otra tabla. Por ejemplo:  Los estudiantes (En la tabla estudiantes) se relacionan con Cursos (Tabla de cursos). Un estudiante puede tener muchos cursos y un curso puede tener muchos estudiantes.  
###### En estos casos se suele crear una tabla intermedia que relacione cada estudiante con su curso, por ejemplo. 


---

# Ejecutar archivos .sql: 

- ## Para MySQL: 
```shell
mysql -u usuario -p < archivo.sql
```

- ## Para PostgreSQL: 
```shell
psql -U usuario -f archivo.sql
```

- ## Para SQL Server: 
```shell
sqlcmd -S servidor -U usuario -P contraseña -i archivo.sql
```

- ## Para Oracle: 
```shell
sqlplus usuario/contraseña@nombre_instancia @archivo.sql
```

# Funcionamiento interno 
## Operadores logicos vs Operadores de comparación

#### Operadores de comparación ( < , > , <= , >=, != , =, between, like)
##### Estos comparadores devuelven un booleano (TRUE o FALSE)

#### Operadores lógicos ( AND , OR , NOT, IN )
##### Estos comparadores comparan entre booleanos tambien devuelviendo TRUE o FALSE

#### La diferencia es que los operadores de comparación comparan valores arrojando true o false, mientras que los operadores logicos comparan booleanos.  
