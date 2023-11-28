----
- Tags: #tecnologías
-----
# Organización del código en módulos

La organización del código en módulos es una práctica esencial en Python para construir programas escalables y mantenibles. Los módulos son archivos de Python que contiene definiciones y declaraciones de variables, funciones, clases u otros objetos que se pueden reutilizar en diferentes partes del programa.
###### Estructura de Módulos

Cada módulo en Python es un archivo **.py** que encapsula tu código para un propósito especifico. Por ejemplo, puedes tener un módulo para operaciones matemáticas, otro para manejo de entradas/salidas, y otro para la lógica de la interfaz de usuario. esta estrucutar ayuda a mantener el código organizado, facilita la lectura y hace posible reutilización de código.
###### Importación de Módulos

Python utiliza la palabra clave **import** para utilizar módulos. Puedes importar un módulo comleto, como **import math** o importar nombres específicos de un módulo utilizando **from math import sqrt**. Python también permite la importación de módulos con una alias para facilitar su uso dentro del código, como **import numpy as np**.
###### Paquetes

Cuando los programas crece y los módulos comienzan a acumularse, Python permite organizar módulos en patquetes. Un paquete es una carpeta que contiene módulos y un archivo especial llamado **__init__.py**, que indica a Python que esa carpeta contiene módulos que pueden ser importados.

**Ventajas de los Módulos**
- *Mantenimiento*: Los módulos permiten trabajar en partes del código de manera independiente sin afectar otras partes del sistema.
- *Espacio de Nombres*: Los módulos definen su propio espacio de nombres, lo que significa que puedes tener funciones o clases con el mismo nombre en diferentes módulos sin conlicto.
- *Reutilización*: El código escrito en módulos puede ser reutlizado en diferentes programas simplemente importándolos donde se necesite.

Ejemplos de **módulos**:

operations.py
```python
def sum(num1, num2):
	return num1 + num2

def rest(num1, num2):
	return num1 - num2
```

main.py
```python
import operations as op

print(op.sum(42, 43)) # 85
```

- Para listar los módulos integrados por python podríamos ejecutar `import sys; print(sys.builtin_module_names)`.
- Para listar la ruta del sistema de un módulo instalado e importado, podríamos ejecutar `import hashlib; print(hashlib.__file__)`.