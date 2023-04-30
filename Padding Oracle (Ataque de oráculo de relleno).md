-------- 
- Tags: #ataques #basico #teoria #practica
---- 

# ¿ Que es el **Padding Oracle** ? 

### Este ataque es un ataque contra datos cifrados que permite al atacante **descifrar** el contenido de los datos **sin conocer la clave**. 

### Un "**oráculo**"  hacer referencia a una "indicación" que brinda a un atacante información sobre si la acción que ejecuta es correcta o no. 

### El "**relleno**" es un término criptográfico especifico. Algunos cifrados, que son los algoritmos que se usan para cifrar los datos, funcionan en *bloques de datos* en los que cada bloque tiene un tamaño fijo. Si los datos que deseas cifrar no tienen el tamaño adecuado para rellenar los bloques, los datos se **rellenan** automáticamente hasta que lo hacen. Muchas formas de relleno requieren que este siempre esté presente, incluso si la entrada original tenía el tamaño correcto. Esto permite que el relleno siempre se quite de manera segura tras el descrifrado. 

### Al combinar ambos elementos, una implementeación de software con un oráculo de relleno revela si los datos descrifrados tienen un relleno válido. El oráculo podría ser algo tan sencillo como devolver un valor que dice "Relleno no válido", o bien algo más complicado como tomar un tiempo considerablemente diferente para procesar un bloque válido en lugar de uno no válido. 

### Los cifrados basados en bloques tienen otra propiedad, denominada "**modo**", que determina la relación de los datos del primer bloque con los datos del segundo bloque, y así sucesivamente. Uno de los modos más usados es **CBC**. Este representa un bloque aleatorio inicila, conocido como "**vector de inicialización (IV)**", y combina el bloque anterior con el resultado del cifrado estático a fin de que cifrar el mismo mensaje con la misma clave no siempre genere la misma salidad cifrada.

### Un atacante puede usar un or+aculo de relleno, en combinación con la manera de estrucutrar los datos de CBC, para enviar mensajes ligeramente modificados al código que expone el oráculo y seguir enviando datos hasta que el oráculo indique que son correctos. Desde esta respuesta, el atacante puede descifrar el mensaje byte a byte. 

### Las redes informáticas modernas son de una calidad tan alta que un atacante puede detectar diferencias muy pequeñas (menos de 0,1 ms) en el timepo de ejecución en istemas remotos. Las aplicaciones que suponen que un descrifrado correcto solo puede ocurrir cuando no se alteran los datos pueden resultar vulnerables a ataques desde herramientas que están diseñadas para observar diferencias en el descrifrado correcto e incorrecto. Si bien esta diferencia de temporalización puede ser más significativa en algunos lenguajes o bibliotecas que en otros, ahora se cree que se trata de una amenaza práctica para todos los lenguajes y las bibliotecas cuando se tien en cuenta la respuesta de la aplicación ante el error. 

