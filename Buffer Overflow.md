## Memoria RAM
---
La memoria RAM es una memoria volatil (Esto significa que cuando deja de recibir corriente se borra) de acceso aleatorio de almacenamiento a corto plazo. Esta sirve para almacenar de forma temporal todos los programas y sus procesos de ejecucción.

![[MemoriaRam.png]]

## Informe: Buffer Overflow
---
Un Buffer Overflow es un tipo de falla de seguridad que se produce cuando se escriben más datos en un búfer (un espacio en la memoria) de los que puede contener, lo que resulta en la sobreescritura de los datos en las áreas adyacentes del búfer y puede dar como resultado la ejecución no intencionada de código malicioso, la corrupción de datos o una interrupción del sistema. 

## Registros en un Buffer Overflow 
--- 
Un Buffer Overflow típicamente se produce en una aplicación que está escribiendo en un búfer sin verificar el tamaño de la entrada de datos. En un sistema operativo de tipo Unix, la memoria está organizada en una pila, que se utiliza para almacenar los valores de los registros y la información sobre la ubicación del código que se está ejecutando en un momento dado. 

Aquí es donde entran en juego los registros #EIP, #ESP y #EBP: 

- #### #EIP (Instruction Pointer): es un registro que apunta a la dirección de la memoria que contiene la próxima instrucción a ejecutar. 

- #### #ESP (Stack Pointer): es un registro que apunta a la parte superior de la pila, donde se encuentran los valores de los registros y la información sobre la ubicación del código. 

- ##### #EBP (Base Pointer): es un registro que se utiliza para mantener un seguimiento de la posición de la pila y para acceder a los valores almacenados en la pila. 

Cuando se produce un Buffer Overflow, los datos maliciosos pueden escribirse en la memoria adyacente a un búfer y pueden sobrescribir los valores de los registros #EIP, #ESP y #EBP, lo que puede causar la ejecución no intencionada de código malicioso o la corrupción de datos. 

![[StackMemoriaRam.png]]

## Conclusión 
--- 
En conclusión, un Buffer Overflow es una falla de seguridad crítica que puede resultar en la ejecución no intencionada de código malicioso, la corrupción de datos o una interrupción del sistema. Los registros #EIP, #ESP y #EBP son cruciales para comprender cómo un Buffer Overflow puede afectar el funcionamiento normal de un sistema y cómo se puede abusar de esta falla de seguridad para ejecutar código malicioso. Es importante tomar medidas para prevenir y mitigar los Buffer Overflows, incluyendo la verificación de los tamaños de entrada de datos y la implementación de controles de seguridad adicionales. Además, es importante mantener actualizados todos los software y sistemas operativos, ya que las soluciones de seguridad y los parches para corregir fallas de seguridad, incluyendo los Buffer Overflows, a menudo están disponibles a través de actualizaciones de software. La educación y concienciación sobre la importancia de la seguridad informática también es fundamental para prevenir y mitigar los Buffer Overflows y otras fallas de seguridad. 

Es importante destacar que los Buffer Overflows no solo afectan a las aplicaciones y sistemas operativos, sino que también pueden afectar a los dispositivos IoT (Internet de las cosas), que cada vez son más comunes en nuestra vida diaria. Por lo tanto, es esencial ser consciente de los riesgos de seguridad asociados con los Buffer Overflows y tomar medidas para prevenirlos y mitigarlos.

![[Pasted image 20230210235010.png]]