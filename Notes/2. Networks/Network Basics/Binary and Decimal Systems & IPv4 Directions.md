# Binary Directions & IPv4

Las direcciones IPv4 comienzan como binarias, una serie de solo 1 y 0. Estos son difíciles de administrar, por lo que los administradores de red deben convertirlos a decimales. Como sabemos el sistema *binario* ([[0. Binary]]) es un sistema de numeración base 2 que consta de los dígitos 0 y 1, llamado *bits*.

Es importante la comprensón de este sistema, ya qeu los hosts, los servidores y los disposiitivos de red usan el direccionamiento binario. Específicamente, usan direcciones IPv4 binarias, como se muestra en esta imágen:

![[binary_directions_ipv4_example_image.png]]

Cada dirección consta de una cadena de 32 bits, divididos en cuatro secciones denominadas *octetos*. Cada octeto contiene *8 bits* (o *1 byte*) separadas por un punto. Por ejemplo, a la PC1 de la imagén se le asignó la dirección IPv4 *11000000.10101000.00001010.00001010*. La dirección de gateway predeterminado sería la interfaz Gigabit Ethernet del R1, *11000000.10101000.00001010.00000001*.

Este sistema funciona muy bien con hosts y dispositivos de red. Sin embargo, como vemos es muy difícil para nosotros los humanos trabajar con este.

Para facilitar el uso, las direcciones IPv4 se expresan comúnmente en notación decimal con puntos. A la PC1 se le asgina la dirección *192.168.10.10*, y como gateway predeterminado se le asigna la dirección *192.168..10.1*:

![[decimal_directions_ipv4_example_image.png]]

----
# Binary and Decimal position notation

Para aprender a convertir de sistema binario a decimal, es necesario entender la notación de posición. El término "*notación de posición*" signigica que un dígito representa diferentes valores según la "posición" que el dígito ocupa en la secuencia de números. 

El **sistema decimal** es un sistema *base 10*, lo que ínidica que esta base númerica, también denominada *radix*, se basa en 10.

| Radix    | 10   | 10   | 10   | 10   |
| -------- | ---- | ---- | ---- | ---- |
| Position | 3    | 2    | 1    | 0    |
| Calc     | 10^3 | 10^2 | 10^1 | 10^0 |
| Value    | 1000 | 100  | 10   | 1    |
`Base 10 - (0,1,2,3,4,5,6,7,8,9)`

Para calcular el valor posicional se toma la raíz (radix) y se la elevá por el valor exponencial de su posición. Así mismo, para usar el sistema de posición, hay que unir el número con su valor de posición, por ejemplo, con el número *1234* sería:

| Radix    | 10      | 10     | 10    | 10   |
| -------- | ------- | ------ | ----- | ---- |
| Position | 3       | 2      | 1     | 0    |
| Decimal  | 1       | 2      | 3     | 4    |
| Value    | 1000    | 100    | 10    | 1    |
| Calc     | 1\*1000 | 2\*100 | 3\*10 | 4\*1 |
| Result   | 3000+   | 200+   | 30+   | 4    |

Teniendo en cuenta esto, el **sistema binario** es un sistema *base 2*, lo que índica que la base númerica se basa en 2.

| Radix    | 2   | 2   | 2   | 2   | 2   | 2   | 2   | 2   |
| -------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Position | 7   | 6   | 5   | 4   | 3   | 2   | 1   | 0   |
| Calc     | 2^7 | 2^6 | 2^5 | 2^4 | 2^3 | 2^2 | 2^1 | 2^0 |
| Value    | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
`Base 2 - (0,1)`

De igual manera, para calcular el valor posicional se toma la raíz y se la elevá por el valor exponencial de su posición. Por ejemplo, a continuación se mostrará como se puede convertir a decimal el valor del número binario *11000000*, obteniendo como resultado el número decimal *192*:

| Radix    | 2      | 2     | 2     | 2     | 2    | 2    | 2    | 2    |
| -------- | ------ | ----- | ----- | ----- | ---- | ---- | ---- | ---- |
| Position | 7      | 6     | 5     | 4     | 3    | 2    | 1    | 0    |
| Binary   | 1      | 1     | 0     | 0     | 0    | 0    | 0    | 0    |
| Value    | 128    | 64    | 32    | 16    | 8    | 4    | 2    | 1    |
| Calc     | 1\*128 | 1\*64 | 0\*32 | 0\*16 | 0\*8 | 0\*4 | 0\*2 | 0\*1 |
| Result   | 128+   | 64+   | +0    | +0    | +0   | +0   | +0   | +0   |

Una vez entendido esto,  por cada octeto de una dirección IP se puede aplicar la misma lógica para resolver cada valor decimal de cada octeto.

----
# Decimal System convertion to Binary

También es necesario entender cómo convertir una dirección IPv4 decimal punteada a una binaria. Para esto deberemos válidar por cada octeto cada posición de la tabla de valores binarios y contemplar si el número del primer octeto es mayor o menor al bit más signifiativo (128), si no es se colocará un 0 en el valor posicional del 128, de lo contrario, se agregara un 1 y se restara el valor posicional 128 al número del octeto, y así se continuará hasta quedar con el valor de 0 y hallar con conversión en sistema binario.

Para poder comprender este proceso mejor, vamos a utilizar de ejemplo la dirección IPv4 *192.168.11.10*.

En este caso utilizaremos el primer y segundo octeto dado que el tercer y cuarto octeto (11 y 10) son relativamente sencillos de calcular, por lo cual rápidamente podemos saber que los valores binarios de estos equivalen a *00001011* y *00001010*.

- Primer octeto (**192**)

¿El primer octeto número 192 es igual o mayor a el bit más significativo 128? Como es el caso, añadiremos un 1 al valor posicional del bit más significativo y restaremos 128 al valor inicial de 192, lo que nos deja como resultado un resto de 64.

![[decimal_to_binary_octet_example_image_1.png]]

Ahora continuaremos con nuestro resto, el cual es 64 y lo que nos debemos preguntar es, ¿64 es igual o mayor que el siguiente bit (64)? Como nuevamente la respuesta es si, agregamos un 1 al siguiente valor posicional de alto orden y restamos el valor posicional 64 a nuestro resto, 64, lo que nos deja en 0, y como nuestro resto es 0, en las siguientes posiciones restantes agregaremos un 0. 

![[decimal_to_binary_octete_example_image_2.png]]

- Segundo octeto (**168**)

¿El primer octeto número 168 es igual o mayor a el bit más significativo 128? Como es el caso, añadiremos un 1 al valor posicional del bit más significativo y restaremos 128 al valor inicial de 192, lo que nos deja como resultado un resto de 40.

![[decimal_to_binary_second_octet_example_image_1.png]]

Ahora continuaremos con nuestro resto, el cual es 40 y lo que nos debemos preguntar es, ¿40 es igual o mayor que el siguiente bit (64)? Como la respuesta es no, agregaremos un 0 binario en el valor posicional 64 y continuaremos con los demás valores posicionales.

![[decimal_to_binary_second_octet_example_image_2.png]]

Todavía con nuestro resto 40, nos preguntamos ¿Es 40 igual o mayor que el siguiente bit (32)? Como la respuesta es si agregaremos un 1 binario en dicho valor posicional y restaremos nuestro resto con este valor (40-32) lo que nos deja un nuevo resto de 8.

![[decimal_to_binary_second_octet_example_image_3.png]]

Continuando con nuestro nuevo resto, 8 nuevamente nos preguntamos ¿Es 8 igual o mayor que el siguiente bit (16)? Como la respuesta es no, agregaremos un 0 binario en el valor posicional 16 y continuaremos con los demás valores posicionales.

![[decimal_to_binary_second_octet_example_image_4.png]]

Continuando con nuestro resto, el cual es 8 nos preguntamos, ¿8 es igual o mayor que el siguiente bit (8)? Como la respuesta es si, agregamos un 1 al siguiente valor posicional de alto orden y restamos el valor posicional 8 a nuestro resto, 8, lo que nos deja en 0, y como nuestro resto es 0, en las siguientes posiciones restantes agregaremos un 0. 

![[decimal_to_binary_second_octet_example_image_5.png]]

---
# IPv4 Directions

Como mencionamos al principio de este tema, los routers y las computadoras solo entienden binario, mientras que los humanos trabajamos en decimal. Por esto es importante entender a fondo estos dos sistemas de numeración y cómo se utilizan en redes.

Para cerrar, entonces sabemos que las direcciones IPv4 las leemos diariamente en formato decimal punteado, como por ejemplo *192.168.10.10*. Pero esta dirección IP consta de 4 octeteos, es decir, cuatro segmentos de 8 bits cada uno:

![[4_octets_example_image_ipv4_directions.png]]

Y por ende, entendemos que estas direcciones comúnmente utilizadas son direcciones de *32 bits* en total:

![[32_bits_example_image_ipv4_directions.png]]