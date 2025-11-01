----
- Tags: #tecnologías
-----
# Librerías OS y SYS

Las bibliotecas *os* y *sys* de Python son herramientas esenciales para cualqier desarrollador que busque interactuar eficazmente con el sistema operativo y gestionar el entorno de ejecucción de sus porgramas. estas bibliutoecas proporcionan una ampia gama de funcinalidaddes que permiten una mayor flexibilidad y control en el desarrollo de software.

-----
# Biblioteca **os**

La biblioteca **os** en Python es una herramienta poderosa para interactuar con el sistema operatvio. Proporciona una interfaz portátil para usar funcionalidades del sistema operativo, lo que significa que los programas pueden funcionar en diferentes sistemas operativos sin cambios significativos en el código. Algunas de sus capacidades incluyen:

- **Manipulación de Archivos y Directorios**: Permite realizar operaciones como crear, eliminar, mover archivos y directorios, y consultar sus propiedades.
- **Ejecución de Comandos del Sistema**: Facilita la ejecución de comandos del sistema operativo desde un programa Python.
- **Gestión de Variables de Entorno**: Ofrece funciones para leer y modificar las variables de entorno del sistema.
- **Obtención de Información del Sistema**: Proporciona métodos para obtener información relevante sobre el sistema operativo, como la estructura de directorios, detalles del usuario, procesos, etc.

Ejemplos:
```python
import os 

os.getcwd() # pwd 
os.listdir('/path/') # ls 
os.mkdir('name') # mkdir name 
os.path.exists('file') # True | False
os.getevn('PATH') # echo $PATH
```

----
# Biblioteca **sys**

la biblioteca **sys** en Python es fundamental para interactuar con el entorno de ejecución del programa Python. A difererencia de **os**, que se centra en el sistema operativo, **sys** está más roientada a la interacción con el intérprete de Python. Sus principales usos son: 

- **Argumentos de Línea de Comandos**: Permite acceder y manipular los argumentos que se pasan al programa Python desde la línea de comandos.
- **Gestión de la Salida del Programa**: Facilita el control sobre la salida estándar (**stdout**) y la salida de error (**stderr**), lo cual es esencial para la depuración y la presentación de resultados.
- **Información del Intérprete**: Ofrece acceso a configuraciones y funcionalidades relacionadas con el intérprete de Python, como la versión de Python en uso, la lista de módulos importados y la gestión de la ruta de búsqueda de módulos.

Ejemplos
```python
import sys

sys.exit(0)
sys.argv[0] # Script name 
len(sys.argv)
sys.path
```