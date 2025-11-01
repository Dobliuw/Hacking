----
- Tags: #tecnologías
-----
# Librería **os** y módulo **shutil** 

La librería **os** y el módulo **shutil** en Python son herramientas fundamentales para intercatuar con el sistema de archivos, especialmente en lo que resepcta a la creación y eliminación de archivos y directorios.

----
# Librería os

- **Funcionalidades Básicas**: *OS*  proporciona una interfaz rica y cvariada para interactuar con el sistema operativo subyacente. Permite realizar operaiones como la creación y eliminación de archivos y directorios, así como la manipulación de rutas y el manejo de la información del sistema de archivos.
##### Creación y Eliminación de archivos y directorios

- **Creación de directorios**: Utilizando **os.mkdir()** u **os.makedirs()**, se pueden crear directorios individuales o múltiplies.
- **Eliminación**: **os.remove()** se usa para eliminar archivos, mientras que **os.rmdir()** y **os.removedirs** permiten eliminar directorios y directorios con subdirectorios, respectivamente.
- **Gestión de rutas**: La sublibrería **os.path** es crucial para manipular rutas de archivos y directorios, como unir rutas, obtener nombres de archivos, verficicar si un archivo o directorio existe, etc.

```python
import os 

os.path.exists("file") # Search a file in actual dir
os.mkdir("dobliuw") # Create dobliuw directory
os.makedirs("dobliuw_a/dobliuw_b") # Create dobluw_a directory with dobliuw_b subdirectory 
os.listdir() # [dobliuw, dobliuw_a]
os.remove("file.txt") # Remove a file 
os.rmdir("dobliuw") # Remove a empty dir 
os.rename("file", "file_edited") # Change a name
os.path.getsize("/etc/passwd") # Get a file size 
os.path.join("mi_dir", "mi_file.txt") # mi_dir/mi_file.txt
os.path.basename("/etc/hosts") # Hosts
os.path.dirname("/etc/hosts") # /etc
directory, file = os.path.split("/etc/hosts") # /etc , hostss
``` 
----
# Módulo shutil

- **Operaciones de alto nivel**: Mientras que os se enfoca en operaciones básicas, **shutil** porporciona funciones de nivel superior, más orientadas a tareas complejas y operaciones en lotes.
- **Copiar y Mover arhcivos y directorios**: *SHUTIL* es especialmente útil para copiar y mover archivos y directorios. Funciones como **shutil.copy()**, **shutil.copytree()** y **shutil.move()** facilitan estas tareas.
- **Eliminación de directorios**: Aunque *os* puede eliminar directorios, **shutil.rmtree()** es una herramienta más poderosa para eliminar un directorio completo y todo su contenido.
- **Manejo de archivos temporales**: *shutil* también ofreffce funcionalidades para trabajar con archivos temporales, lo que es útil para operaciones que requieren almacenamiento temporal de datos.

```python
import shutil

shutil.rmtree("directory") # Remove all files and dirs 
```