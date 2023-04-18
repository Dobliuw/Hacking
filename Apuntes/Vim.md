--- 
- Tags: #editordetexto #atajos 
---

# ¿ Que es ?

## Vim es un editor de textos, muy famoso porque es para terminal y porque tiene unas combinaciones de teclas muy potentes, aunque complejas de aprender. Viene como evolución a otro editor muy similar, usado en UNIX, llamado **Vi**.
## Vim, aunque tiene modo gráfico donde más se usa es directamente desde la terminal. Esto para muchos es una ventaja porque pueden trabajar desde una conexión SSH en un servidor en remoto.

## Otro punto diferenciador de Vim es que está centrado en el teclado. Auque existen config y plugins para hacerlo funcionar con el ratón, la gracia es usarlo con el teclado porque así ahorras tiempo.

----

# Convinación de teclas:


- ## Teclas [ Alt + u ]
### Funciona como un **Ctrl + z**, vuelve para atras el utlimo cambio.

- ## Teclas [ Alt + v ] 
### Permite poner en modo **visual** el editor para **trabajar** sobre una selección **texto**.

- ## Teclas [ Esc + : ]
### Permite ingresar al modo para insertar **comandos**. 

- ## Teclas [ Esc + / ] 
### Permite al usuario ingresar una string para **buscar coincidencias**. 

- ## Tecla [ i ]
### Modo **interactivo**, permite al usuario escribir.

- ## Tecla [ 0 ] 
### Lleva el **cursor** del usuario hasta el **principio** de la línea en la que se encuentra. 

- ## Tecla [ $ ] 
### Lleva el **cursor** del usuario hasta el **final** de la línea en la que se encuentra.}

- ## Tecla [ w ]
### Lleva el **cursor** del usuario hasta la siguiente **palabra**. 

- ## Tecla [ y ]
### Con una **selección** previamente hecha funciona para **copiar** la misma y **sin** selección para copiar **todoa la línea**.

- ## Tecla [ p ]
### **Pega** lo que este en la clipboard del usuario.

- ## Tecla [ o ]
### **Inserta** una nueva **línea**.

- ## Tecla [ j ]
### **Bajar** a la línea de abajo.

- ## Teclas [ d + d ]
### **Eliminar** líneas, palabras, selecciones, se convinan con teclas.

- ## Tecla [ . ]
### **Repetir** lo **ultimo** se realizo.

- ## Modo de remplazar valores 
### Supongamos que tengoa mucho texto separado por , y quiero remplazarlo por un salto de línea: 
## Tecla [ Esc + : ] +  %s/{valor_to_change}/{new_value}

## Ejemplo: 
#### Tecla [ Esc + : ] + %s/,/\r 
### En el ejemplo de arriba remplazamos la , ( /,/ )  con un salto de línea ( /\r ). 

- ## Convinar teclas 
### Con los números y las teclas anteriormente vistas se pueden realizar convinaciónes muy potentes: 

## Ejemplos: 

### [ d +  2  + w ] --> Eliminar 2 palabras.
### [ 3 + d + d ] --> Eliminar 3 líneas.
### [ 3 + w ] ------> Moverse 3 palabras a la derecha.
### [ d + w ]  -----> Eliminar palabra.
