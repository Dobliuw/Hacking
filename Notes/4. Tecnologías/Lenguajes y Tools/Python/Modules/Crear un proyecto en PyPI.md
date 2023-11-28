# PyPI

El **Python Paxkage Index** (**PyPI**) es el repositorio de software oficial para aplicaciones de terceros en el lenguaje de programación Python. Los desarrolladores de Python pretenden que sea un catálogo exhaustivo de todos los paquetes de Python escritos en código abiertoPyPI.

----
# Creación de paquetes

Antes de poder subir nuestros paquetes de código y módulos a PyPI es necesario comprender como se da la creación de paquetes en Python.
###### Estructura de Directorios

La estructura típica de un paquete podría incluir directorios para documentación, pruebas y el propio código, así como archios de configuración para la instalación y la distribución del paquete.

```bash
mkdir my_project && cd my_project

mkdir package_name
touch README.md setup.py
```

Para dar comienzo a la estrucutra de los proyectos de software, solemos tener carpetas por cada paquete, siendo este el que contiene varios módulos. Por otro lado, archivos que podemos encontrarnos en proyectos suelen ser el **README.md**, archivo escrito en *mark down* que suele tener una descripción del uso y definición del proyecto; por otro lado el archivo **setup.py**, utilizado para poder configurar el proyecto para su release.

```bash
cd package_name
touch __init__.py
nano example.py
```

En este ejemplo, nos dirigimos a la carpeta previamente creada con el nombre de nuestro paquete (**package_name** en este caso) y creamos por un lado un archivo con nombre **__init__.py**, archivo el cual tendrá como finalidad permitirle a Python entender e inicializar el *paquete*, a su vez, este archivo suele utilizarse para facilitar la importación de módulos, debido a que si tenemos muchos paquetes y módulos para realizar la importación de ciertos módulos tendremos que aclarar el paquete. 
Por otro lado crearemos un modulo con un nombre que nos interese, en este ejemplo **example.py**, módulo el cual tendrá su respectivo código según lo que búsquemos, tanto declaraciones de funciones, clases, variables, etc.

De esta manera, teniendo en consideración el siguiente ejemplo de módulo, el contenido del archivo **__init__.py** podría ser el siguiente:

example.py
```python
def example_fun():
	print("This is an example.")
```

\_\_init\_\_.py
```python
from .example import *
```

De esta manera, si fuera de la carpeta "*package_name*" de nuestro paquete, importaramos la función example, podríamos hacerlo de la siguiente manera:

```python
from package_name import example_fun
```

En caso de no contar con el archivo **__init__.py**, deberíamos realizar la importación de la siguiente manera:

```python
from package_name.example import example_fun
```

----
# Creación de proyecto en PyPI

Una vez entendido como se crean los paquetes y los módulos, podemos proseguir suponiendo que ya tenemos nuestro proyecto finalizado y simplemente queremos subirlo al Indexador de Paquetes de Python (PyPI) para que nuestro paquete este disponible y pueda ser instalado con **pip** por ejemplo, continuando con el ejemplo de proyecto llamado "*my_project*", con el comando `pip3 install my_project`.
###### Creación de cuenta en [PyPi](https://pypi.org/) 

Para poder subir un proyecto a la página de PyPI lo primero que tendremos que realizar es la creación de nuestra cuenta junto a la vinculación de la misma a nuestro número de telefono.
###### Creación de Token

Una vez creada nuestra cuenta y logueados en ella, deberemos dirigirnos a la opción **profile** > **accounts settings** > **API Tokens** > **Add API token** y le ingresamos un nombre seguido de crear el mismo.
###### Configuración de archivo .pypirc

Una vez que tengamos nuestra cuenta y el API token generado, procederemos a crear el archivo **.pypirc** en el directorio del usuario administrador.

```bash
sudo nano /root/.pypirc
```

.pypirc
```bash
[pypi]
	username = __token__
	password = {token_created_here}
```
###### Configuración de archivo setup.py

Como se menciono en la parte de cración de paquetes, dentro de nuestro proyecto solemos crear un archivo llamado **setup.py** con la finalidad de poder configurar el proyecto para sus releases.

setup.py
```python
from setuptools import setup, find_packages

with open("README.md", "r", encodigin="utf-8") as frm:
	long_description = frm.read()
	
setup(
	name="{proyect_name}",
	version="0.1.0",
	packages=find_packages(),
	install_requires=[],
	author="Dobliuw",
	description="{proyect_description}",
	long_description=long_description,
	long_description_content_type="text/markdown",
	url="{some_url_about_your_proyect}"
)
```

Una vez realizado todos estos pasos, solo quedaría subir nuestro proyecto:

```bash
pip3 install twine

python3 -m build

twine upload dist/* --verbose
```

Una vez realizado esto, en nuestro perfil de **PyPI** se subiria nuestro proyecto.