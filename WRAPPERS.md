----
- Tags: #basico #teoria #practica
----

# Wrappers 

- ## Representar recursos en base64 

### Esto sirve para apuntar a recursos y mostrarlos en base64, sobre todo para archivos .php los cuales se interpretan por el navegador. 

### `php://filter/convert.base64-encode/recourse=index.php`

### De esta manera podriamos copiar la cadena base64, guardarlo en un archivo y luego con `cat file | base64 -d | sponge file` lo decodeamos y volvemos a guardar en el mismo archivo.

### Tambien existen otros como `php://filter/read=string.rot13/resource=index.php` y luego con comandos de bash comp `cat {data} | tr '[c-za-bC-ZA-B]' '[p-za-oP-ZA-O]'` podriamos obtener el resultado final.