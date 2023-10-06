-----------
- Tags: #editordetexto #atajos 
---

# ¿ Que es ?

## Vim es un editor de textos, muy famoso porque es para terminal y porque tiene unas combinaciones de teclas muy potentes, aunque complejas de aprender. Viene como evolución a otro editor muy similar, usado en UNIX, llamado **Vi**.
## Vim, aunque tiene modo gráfico donde más se usa es directamente desde la terminal. Esto para muchos es una ventaja porque pueden trabajar desde una conexión SSH en un servidor en remoto.

## Otro punto diferenciador de Vim es que está centrado en el teclado. Auque existen config y plugins para hacerlo funcionar con el ratón, la gracia es usarlo con el teclado porque así ahorras tiempo.

----

# Convinación de teclas:


- ## Teclas [ Alt + u ]
Funciona como un **Ctrl + z**, vuelve para atrás el ultimo cambio.

- ## Teclas [ Alt + v ] 
Permite poner en modo **visual** el editor para **trabajar** sobre una selección **texto**.

- ## Teclas [ Esc + : ]
Permite ingresar al mvodo para insertar **comandos**. 

- ## Teclas [ Esc + / ] 
Permite al usuario ingresar una string para **buscar coincidencias**. 

- ## Tecla [ i ]
Modo **interactivo**, permite al usuario escribir.

- ## Tecla [ 0 ] 
Lleva el **cursor** del usuario hasta el **principio** de la línea en la que se encuentra. 

- ## Tecla [ $ ] 
Lleva el **cursor** del usvuario hasta el **final** de la línea en la que se encuentra.}

- ## Tecla [ w ]
Lleva el **cursor** del usuario hasta la siguiente **palabra**. 

- ## Tecla [ y ]
Con una **selección** previamente hecha funciona para **copiar** la misma y **sin** selección para copiar **todoa la línea**.

- ## Tecla [ p ]
**Pega** lo que este en la clipboard del usuario.

- ## Tecla [ o ]
**Inserta** una nueva **línea**.

- ## Tecla [ j ]
**Bajar** a la línea de abajo.

- ## Teclas [ d + d ]
**Eliminar** líneas, palabras, selecciones, se combinan con teclas.

- ## Tecla [ . ]
**Repetir** lo **ultimo** se realizo.

- ## Modo de remplazar valores 
Supongamos que tengo mucho texto separado por , y quiero remplazarlo por un salto de línea: 
## Tecla [ Esc + : ] +  %s/{valor_to_change}/{new_value} 
Esto para remplazar el primer valor a cambiar por un nuevo valor, si quisiera aplicarlo para todos los matches debería agregar **/g** al final.

## Ejemplo: 
#### Tecla [ Esc + : ] + %s/,/\r 
En el ejemplo de arriba remplazamos la , ( /,/ )  con un salto de línea ( /\r ). 

- ## Combinar teclas 
Con los números y las teclas anteriormente vistas se pueden realizar combinaciones muy potentes: 

## Ejemplos: 

[ d +  2  + w ] --> Eliminar 2 palabras.
[ 3 + d + d ] --> Eliminar 3 líneas.
[ 3 + w ] ------> Moverse 3 palabras a la derecha.
[ d + w ]  -----> Eliminar palabra.

## Macros: 

Los macros son una secuencia de teclas que se repiten continuamente, los cuales se pueden grabar para posteriormente indicar que la secuencia de teclas grabada se realice un total de x veces. 

Estos se pueden grabar con para una tecla en particular, por ejemplo, quiero hacer que a la hora de realizar un [ Esc ] + [ o ] se realice lo siguiente: 

print("Dobliuw")

Por lo que podría presionar [ Esc ] + [ q ] + [ {tecla_to_macro} ] para indicar que quiero guardar un macro de lo que voy a realizar en la letra {{tecla_to_macro}}( [ o ] ) en el ejemplo mencionado. 

Una vez presionado las teclas indicadas aparecerá *recording @{tecla_to_macro}* (*recording @o*), lo cual nos indica que estamos grabando una secuencia de teclas dentro de la letra "o". 

Una vez finalizada la secuencia de teclas que nos interesa realizar, tocamos [ Esc ] + [ q ], y habríamos guardado la secuencia de teclas ingresada bajo la letra ingresada ( [ o ] ). 

Para indicar que queremos que se realice el macro guardado lo hacemos con [ Esc ] + [ @ ] + [ {tecla_to_macro} ] ( [ Esc ] + [ @ ] + [ o ] )
