# Command IOS syntax

| Convention     | Description                                                                                                                                                                      |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **negrita**    | Indica comandos y palabras clave que se ingresa *literalmente* como se muestran.                                                                                                 |
| *cursiva*      | Indica arguemntos para los cuales *el usuario proporciona el valor*.                                                                                                             |
| `[x]`          | Los corchetes (`[]`) indican un elemento *opcional*, palabra clave o argumento.                                                                                                  |
| `{x}`          | Las llaves (`{}`) indican un elemento *obligatorio*, palabra clave o argumento.                                                                                                  |
| `[x {y \| z}]` | Las llaves y las líneas verticales entre corchetes indican que se requiere dentro de un elemento opcional. Los espacios se utilizan para delinear claramente partes del comando. |

----
# Shortcuts

| Shortcut                             | Description                                                                                                               |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| **Tabulación**                       | Completa una entrada de nombre de comando parcial.                                                                        |
| **Retroceso**                        | Borra el carácter a la izquierda del cursor.                                                                              |
| **Ctrl+D**                           | Borra el caracter donde está el cursor.                                                                                   |
| **Ctrl+K**                           | Borra todos los caracteres desde el cursor hasta el final de la línea de comandos.                                        |
| **Esc D**                            | Borra todos los caracteres desde el cursor hasta el final de la palabra.                                                  |
| **Ctrl+U** o **Ctrl+X**              | Borra todos los caracteres desde el cursor hasta el comienzo de la línea de comando                                       |
| **Ctrl+W**                           | Borra la palabra a la izquierda del cursor.                                                                               |
| **Ctrl+A**                           | Desplaza el cursor hacia el principio de la línea.                                                                        |
| **Flecha izquierda** o **Ctrl+B**    | Desplaza el cursor un carácter hacia la izquierda.                                                                        |
| **Esc B**                            | Desplaza el cursor una palabra hacia la izquierda.                                                                        |
| **Esc F**                            | Desplaza el cursor una palabra hacia la derecha.                                                                          |
| **Flecha derecha** o **Ctrl+F**      | Desplaza el cursor un carácter hacia la derecha.                                                                          |
| **Ctrl+E**                           | Desplaza el cursor hasta el final de la línea de comandos.                                                                |
| **Flecha arriba** o **Ctrl+P**       | Recupera los comandos en el búfer de historial, comenzando con la mayoría comandos recientes                              |
| **Ctrl+R** o **Ctrl+I** o **Ctrl+L** | Vuelve a mostrar el indicador del sistema y la línea de comando después de que se muestra un mensaje de consola recibido. |

Adicionalmente, cuando vemos que el output es `- - More - -`, estaremos viendo un Stdout en modo páginado, con lo cual será útil tener en mente las siguientes teclas:

| Keys                  | Description                                                             |
| --------------------- | ----------------------------------------------------------------------- |
| Tecla **Enter**       | Muestra la siguiente línea.                                             |
| **Barra espaciadora** | Muestra la siguiente pantalla.                                          |
| Cualquier otra tecla  | Termina la cadena que se muestra y vuelve al modo EXEC con privilegios. |

---
# Leave an execution

| Shortcut         | Description                                                                                                                                                                                                         |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ctrl-C**       | Cuando está en cualquier modo de configuración, finaliza el modo de configuración y regresa al modo EXEC privilegiado. Cuando está en modo de configuración, aborta de nuevo al comando como indicador de comandos. |
| **Ctrl-Z**       | Cuando está en cualquier modo de configuración, finaliza el modo de configuración y regresa al modo EXEC privilegiado.                                                                                              |
| **Ctrl-Shift-6** | Secuencia de interrupción multipropósito utilizada para anular búsquedas DNS, traceroutes, pings, etc.                                                                                                              |
