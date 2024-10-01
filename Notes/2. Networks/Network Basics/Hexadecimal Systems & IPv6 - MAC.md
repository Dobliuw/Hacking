# Hexadecimal Directions & IPv6

Para comprender el direccionamiento de IPv4 de nuestra red, es fundamental entender cómo convertir de binario a decimal y vicebersa (Explcado en [[Binary and Decimal Systems & IPv4 Directions]]). Pero actualmente se comienza a visualizar con mayor frecuencia las direcciones IPv6 en nuestras redes. Para entender estas direcciones, debemos ser capaces de convertir *hexadecimal* a *decimal* y viceversa.

Así como el decimal es un sistema de base 10, el *hexadecimal es un sistema de base 16*. El  sistema base 16 consta los dígitos del 0 al 9 y las letras de la A a la F. (Esto se encuentra explicado en mayor detalle en [[1. Hexadecimal]]). 

A continuación la imagén muestra los valores decimales y hexadecimales equivalentes para los binarios desde el 0000 al 1111:

![[decimal_binary_hexadecimal_table_example_image.png]]

Binario y hexadecimal funcionan bien juntos porque es más fácil expresar un valor como un solo dígito hexadecimal qeu como cuatro bits binarios. 

El sistema de numeración hexadecimal se usa en redes para representar *Direcciones IPv6* y *Direcciones MAC Ethernet*.

Las direcciones IPv6 tienen una lontigud de 128 bits y cada 4 bits está representado por un sólo dígito hexadecimal; para un total de 32 valores hexadecimales. Las direcciones IPv6 no distinguen entre mayúsculas y minúsculas, y pueden escribirse de igual manera en ambas maneras.

Como se muestra en la siguiente imagen, el format preferido para escribir una dirección IPv6 es `x:x:x:x:x:x:x:x:`, donde cada `x` consta de cuatro valores hexadecimales. Al hacer referencia a 8 bits de una dirección IPv4, utilizamos el término "octeto". En IPv6, un "*hexteto*" es el término no oficial que se utiliza para referirise a un segmento de 16 bits o cuatro valores hexadecimales. Cada "x" es un único hexteto, 16 bits o cuatro dígitos hexadecimales.

![[ipv6_with_hextets_and_binary_example_image.png]]