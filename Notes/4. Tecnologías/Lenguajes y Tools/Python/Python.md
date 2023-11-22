----
- Tags: #tecnologías
-----
# Python

Python es un lenguaje de programación de alto nivel, interpretado, de propósito general y de sintexis clara y sencilla. Este se ha convertido en uno de los lenguajes de programación más utilizados en el mundo para diversas ramas y tareas, algunas de las características claves de Python son:
- Lenguaje de **Alto Nivel**: Esto quiere decir que está diseñado para ser fácil de leer yescribir. 
- **Interpretado**: Python es un lenguaje interpretado, lo que significa que no se compila directamente a c´dogio máquina. en cambio, el código fuente se ejecuta directamente por un intérprete.

----
# Intérprete

El intérprete de Python es el programa que ejecuta el c´dogio fuente de Python. Hay varios intérpretes de Python disponibles, pero el intérprete oficial es CPython, que está escrito en C. 

-----
# Convenciones

Las convenciones de programación son reglas o pautas que los programadores adoptan para escribir código de manera consistente y legible. Estas convenciones no son necesariamente reglas impuestas por el lenguaje de programación en sí, sino más bien prácticas recomendaddas que la comunidad de programadores ha acordado seguir. Cada lenguaje de programación puede tener diferentes convenciones, tanto para la declaración de variables, funciones, arrays, etc. En este caso claramente Python no es la exepción y cuenta con sus propias convenciones. Algunas de ellas son: 

- **Snake Case** en la **Declaración de funciones**: A la hora de declarar funciones en python, existe una convención la cual recomienda la declaración de los nombres de funciones con la técnica de *snake_case*. 
- **Uper Camel Case** en la **Declaración de Clases** y **Manejo de Exepciones**: En este caso al igual que en la declaración de funciones, para la declaración de clases se recomienda la declaración de los nombres de las mismas con la técnica de *UpperCamelCase*.
- **Screaming Snake Case** en la **Declaración de Constantes**: Para la declaración de constantes, teniendo en cuenta que de por si en Python las constantes no existen, existe en su lugar una convención para entender que las constantes serán variables con nombres en *SCREAMING_SNAKE_CASE*.

-----
# Sintaxis

###### Tipos de datos
Existen múltiples tipos de datos que serán utilizados a lo largo de muchos lenguajes de programación, en el caso de Python, no tratandose de una exepción, contamos con varios tipos de datos.

- **Strings** (Cadenas): Las cadenas son secuencias de caracteres que se utilizan para manejar texto. Son inmutables, lo que significa que una vez creadas, no puedes cambiar sus caracteres individuales.
- **Integers** (Enteros): Números sin parte decimal.
- **Floats** (Flotantes): Números que incluyen decimales.
###### Operaciones 

Como sabemos, las operaciones son funciones matemáticas sobre tuplas que obtienen un resultado, aplicando unas reglas preestablécidas sobre la tupla.

- **Suma** ( \+ ) 
- **Resta** ( \- )
- **Multiplicación** ( \* )
- **División** ( \/ )
- **Módulo** ( \% )

Es importante tener en cuenta que algunas operaciones se pueden dar con otros tipos de datos y no únicamente con **integers** o **floats**, si no también pueden ser vistos con **strings** y **listas**. 

Ejemplo
```python
# Strings
string1 = "Dobliuw"
string2 = "Dumb"

new_string = string1 + " " + string2 # "Dobliuw Dumb"
new_string2 = string2 * 3 # "DumbDumbDumb"

# Lists / Arrays
arr1 = [1, 2, 3, 4, 5]
arr2 = [6, 7, 8, 9, 10]

new_arr = arr1 + arr2 # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

En caso de hacer manejo de números muy grandes, es importante tener en cuenta que se pueden aplicar formateos para dar mayor legibilidad a la hora de leer e interpretar los valores obtenidos como resultado de determinadas operaciones.

Ejemplo:
```python
x = 12
y = 7
z = x ** y

print(f"{:,}".format(z).replace(",", ".")) # 35.831.808
```
## Variables

Una variable es un espacio en memoria representado con un nombre personalizado en el cual podemos alojar datos de todo tipo para consultarlos en otro momento del programa.

Ejemplos:
```python
name = "Dobliuw" # Str
age = 20 # Int
hobbies = ["Skate", "Hacking", "Gaming"] # List
person = {"name": "Dobliuw", "age": 20} # Dictionary
```
## Listas

Las listas son estructuras de datos que nos permiten almacenar secuencias ordenadas de elementos. Son mutables, lo que significa que podemos modificarlas después de su creación, y son dinámicas, permitiéndonos añadir o quitar elementos de ellas. Algunas de las características más claves de las listas en Python son:

- Almacenar datos heterogéneos, es decir, pueden contener elementos de diferentes tipos (enteros, cadenas, flotantes y más) dentro de una misma lista.
- Ser indexadas y crotadas, lo que permite acceder a elementos específicos de la lista directamente a través de su índice.
- Ser anidadas, es decir, una listar puede contener otras listas como elementos, lo que permite crear estrucutras de datos complejas como matrices.
###### Operaciones con Listas

También cubriremos las operaciones fundamentales que se pueden realizar con listas, como:

- Añadir elementos con métodos como **append()** y **extend()**. 
- Eliminar elementos con métodos como **remove()** y **pop()**.
- Ordenar las listas con el método **sort()** o la función incorporada **sorted()**.
- Invertir los elementos con el método **reverse()** o la sintaxis de corte **\[::-1\]**.
- Comprender las comprensiones de listas, una forma *pythonica* de crear y manipular listas de manera concisa y eficiente.

Ejemplo:
```python
attacks = ["DDoS", "SQL Injection", "Deserialization Attack", "NOSQL Injection", "Cross-Site Scripting", "Server-Side Request Forgery"]
attacks.append("Server Side Template Injection") 
#  ["DDoS", "SQL Injection", "Deserialization Attack", "NOSQL Injection", "Cross-Site Scripting", "Server-Side Request Forgery", "Server Side Template Injection"]
attacks.insert(2, "Client Side Template Injection")
#  ["DDoS", "SQL Injection", "Client Side Template Injection", "Deserialization Attack", "NOSQL Injection", "Cross-Site Scripting", "Server-Side Request Forgery", "Server Side Template Injection"]

attacks[1:4] # ["SQL Injection", "Client Side Template Injection", "Deserialization Attack", ]
attacks.sort() 
# ['Client Side Template Injection', 'Cross-Site Scripting', 'DDoS', 'Deserialization Attack', 'NOSQL Injection', 'SQL Injection', 'Server Side Template Injection', 'Server-Side Request Forgery']
attacks.reverse() # attacks[::-1]
# ['Server-Side Request Forgery', 'Server Side Template Injection', 'SQL Injection', 'NOSQL Injection', 'Deserialization Attack', 'DDoS', 'Cross-Site Scripting', 'Client Side Template Injection']
```
## Condicionales 

Los condicionales son estructuras de control que permiten ejecutar diferentes bloques de código dependiendo de si una o más condiciones son verdaderas o falsas (Basandose en la teoria de Bool). En python, las declaraciones condicionales más comunes son **if**, **elif** y **else**. 

- **if**: Evalúa si una condición es verdader y, de ser así, ejecuta un bloque de código.
- **elif**: Abreviatura de **else if**, se utiliza para verificar múltiples expresiones sólo si las anteriores no son verdaderas. 
- **else**: captura caulquier ccaso que no haya sido capturado por las decalaraciones *if* y *elif* anteriores.

Ejemplo:
```python
age = 20

if age > 18: 
	print("\n[+] The age {} is greater than 18.".format(age))
elif age == 18: 
	print("\n[+] The age {} is equal to 18.".format(age))
else: 
	print("\n[+] The age {} is less than 18.".format(age))

# Ternarios
print("You are older" if age >= 19 else "You are younger")
```
###### Operadores lógicos

Los operadores lógicos condicionales se utilizan para añadir condiciones, tanto en los if como en cualquiera de las instrucciones que lleven una condición. En el caso de python existen algunas las cuales son:

- **or**: Ejecutar un código si una condición de las múltiples condiciones existentes se cumple.
- **and**: Ejecutar un código si todas las condiciones de las múltiples existentes se cumplen.
- **not**: Negar una condición.

Ejemplos:
```python
# Simple login example
name = "Dobliuw"
password = "Dobliuw123"
age = 20
token = "dcba"

if name == "Dobliuw" and password == "Dobliuw123":
	# Login success

if (name == "Dobliuw" and password == "Dobliuw123") or token = "dcba":
	# Login success

if "abcd" not in token:
	# Login success
```

## Bucles

Los bucles permiten ejecutar un bloque de código repetidamente mientras una condición sea verdadera o para cada elemento en una secuencia. Los dos tipos principales de bucles que se suelen utilizar en múltiples lenguajes de programación son **for** y **while**. 

- **for**: Se usa para iterar sobre una secuencia (Como puede ser una *lista*, un *diccionario*, una *tupla* o un *conjunto*) y ejecutar un bloque de código para cada elemento de la secuencia. 
- **while**: Ejecuta un blqoue de código repetidamente mientras una condición específica se mantiene verdadera.
###### Control de Flujo en Bucles

Existen declaraciones de control de flujo que pueden modificar el comportamiento de los bucles, como **break**, **continue** y **pass**.

- **break**: Termina el bucle y pasa el control a la siguiente decalaración fuera del bucle.
- **continue**: Omite el resto del c´doigo dentro del bucle y continúa con la siguiente iteración.
- **pass**: No hace nada, se utiliza como una declaración de relleno donde el código eventualmente irá, pero no ha sido escrito todavía.

Ejemplos:
```python
# For loop
arr = [1, 2, True, "Dobliuw", [65, 43]]
dic = {name: "Dobliuw", age: 20}

for pos, elem in enumerate(arr):
	print("\n[!] We'll find {} in the position {}".format(elem, pos + 1))

for key, val in dic:
	print("\n[!] Key {}: value {}".format(key, value))

# While loop
num = 0

while num < 11: 
	print("\n[!] This is a custom for using while, number {}".format(num))
	num += 1

# Nested loop 
arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for i in arr:
	for l in i:
		print("\n[!] The number is: {}".format(l))

# List comprehension 
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

power_of_2 = [num ** 2 for num in arr]
only_odd_nums_power_of_2 = [num ** 2 for num in arr if num % 2 != 0 ]

# Loop control

# Break
for i in range(11):
	if i == 11:
		break
	print(i)
else:
	print("\n[+] Loop ended successfully")
# 1 2 3 4 5 6 7 8 9 10 
# [+] Loop ended succesfylly


for i in range(11):
	if i == 5:
		break
	print(i)
else:
	print("\n[+] Loop ended successfully")
# 1 2 3 4 

# Pass
while True: 
	pass

# Continue
for i in range(11):
	if i == 5:
		continue
	print("\n i")
# 1 2 3 4 6 7 8 9 10
```
## Funciones

Las funciones son bloques de código reutilizables diseñados para realizar una tarea específica. En Python, se definen usando la palabra clave '**def**' s eguida de un nombre descriptivo y personalizado para la función, paréntesis (Que pueden contener parámetros) y dos puntos. Los parámetros son "*variables de entrada*" que pueden cambiar cada vez que se llama a la función. Esto permite a las funciones operar con diferentes datos y producir resultados correspondientes.

Las funciones pueden devolver valores al programa principal o a otras funciones mediante la palabra clave '**return**'. Esto  las hace increíblemente versátiles, ya que pueden procesar datos y luego pasar esos datos modificados a otras partes del programa.

Ejemplo:
```python
def say_hi(name):
	print("\n[+] Hi {}".format(name))

```
## Ámbito de las variables (Scope)

El **Scope** de una variable se refiere a la región de un programa donde esa variable es accesible. En Python, hay dos tipos principales de ámbitos.

- **Local**: Las variables definidas dentro de una función tiene un ámbito local, lo que significa que solo pueden ser accedidas y modificadas dentro de la función donde fueron creadas.
- **Global**: Las variables definicas duera de todas las funciones tienen un ámbito global, lo que signicia que pueden ser accedidas desde cualquier parte del programa. Sin embargo, para modificar una variable globarl dentro de una función, se debe declarar como global. 

Ejemplo: 
```python
# Local Scope
def random_function():
	local_var = "This is an example of a local var"
	print(local_var)

random_function() # This is an example of a local var
print(local_var) # Error 'local_var' is not defined

# Global Scope
global_var = "This is an example of a global var"

def random_function():
	print(global_var) 

random_function() # This is an example of a global var
print(global_var) # This is an example of a global var

# Global and Local Scope
# 1st example
var = "This is an example of a global var"

def random_function():
	var = "This is an example of a local var"
	print(var) 

random_function() # This is an example of a local var
print(var) # This is an example of a global var

# 2nd exmaple
var = "This is an example of a global var"

def random_function():
	global var 
	var = "I'm a global var too but changed in a function"

random_function() # I'm a global var too but changed in a function
print(var) # I'm a global var too but changed in a function

```
## Funciones Lambda (Anónimas)

Las funciones **lambda** son también conocidas como funciones **anónimas** debido a qeu no se les asigna un nombre explícito al definirlas. Se utilzan para crear pequeñas funciones en el lugar donde se necesitan. generalmente para una operación específica y breve. En Python, una función *lambda* se define con la palabra clave '**lambda**', seguida de una lista de argumentos, dos puntos y la expresión que desea evaluar y devolver.

Una de las ventajas de las funciones lambda es su simplicidad sintáctica, lo que las hace ideal para su uso en operaciones que requiere una función por un breve momento y para casos donde la definición de una función tradicional completa sería excesivamente verbosa.

Algunos de los usos comunes de las funciones anónimas son:

- **Con funciones de orden superior**: Como aquilass que requieren otra función como arguemento, por ejemplo **map()**, **filter()** y **sorted()**.
- **Operaciones simples**: Para realizar cálculos o acciones rápidas donde una función completa sería innecesariamente larga.
- **Funcionalidad en línea**: Cuando se necesita una funcionalidad simple sin la necesidad de reutilizar en otro lugar del código.

Ejemplo:
```python
# Numbers ^ 2 
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

print("\n[+] You've here all numbers^2: ")
print(list(map(lambda num: num ** 2, arr))) # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

# Only odd numbers
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

print("\n[+] You've here only the odd numbers:")
print(list(filter(lambda num: num % 2 != 0, arr))) # [1, 3, 5, 7, 9]

# Multiply all positions in array
from functools import reduce 
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

print("\n[+] You've here the result:")
print("{:,}".format(reduce(lambda num1, num2: num1*num2, arr)).replace(",", ".")) # 3.628.800
```
## Manejo de errores y excepciones

Los errores pueden ocurrir por muchas razones: errores de c´doigo, datos de entrada incorrectos, problemas de conectividad, entre otros. En lugar de permitir que un programa falle con un error, Python nos proporciona herramientas para "atrapar" estos errores y manejarlos de manera controlada, evitando así que el programa se detenga inesperadamente y permitiendo reaccionar de manera adecuada.

###### Excepciones

Una **excepción** en Python es un evento que ocurre durante la ejecución de un programa que interrumpe el flujo normal de las instrucciones del programa. Cuando el intérprete se encuentra con una situación que no puede manejar, "arroja" una excepción.

Ejemplo:
```python
# Handle execptions
# Multiple exception in multipe code blocks
try:

	num = 14/0
	string = "Dobliuw"/4
	
except ZeroDivisionError:
	print("You can not divide numbers by zero.")
except TypeError:
	print("You can not split numbers with strings.")
else:
	print("This code will run if there isn't exceptions.")
finally:
	print("This code will always run.")

# Multiple exception in one code

try:
	# .... code
except (ZeroDivisionError, TypeError):
	# .... handle exceptions

# Make exceptions
try:
	num = int(input("[+] Please insert a number: "))
	if num < 0:
		raise Exception("This is a new and default exception. U can't insert negative numbers.")
except ValueError:
	print("\n[!] Please insert a number and not a string.")
```

-----
# String Formating 

Python proporciona varias maneras de formatear cadenas, permitiendo insertar varaibles en ellas, así como controlar el espaciado, alineación y precisión de los datos mostrados. Dentro de estas técnicas existen varías algunas más conocidas y usadas que otras: 
###### Interpolación de cadenas (**%**)

Este método clásico utiliza marcadores de posición como '**%s**' para cadenas, '**%d**' para enteros o '**%f**' para flotantes. 

Ejemplo:
```python
num1 = 4
num2 = 4

print("\n[+] El resultado de %d + %d es %d" % (num1, num2, num1 + num2))
```
###### Método format

Este método, introducido en Python 2.6, permite una mayor flexibilidad y claridad. Utiliza llaves '**{}**' como marcadores de posición dentro de la cadena y puede incluir detalles sobre el formato de la salida. 

Ejemplo:
```python
name = "Dobliuw"
age = 20

print("\n[+] Hi my name is {}".format(name))
print("\n[+] Hi my name is {0} and I'm {} years old. Att. {0}".format(name, age))
```
###### F-Strings (Literal String Interpolation)

Disponible desde Python 3.6, los F-Strings ofrecen una forma concisa y legible de incrustar expresiones dentro de literales de cadena usando la letra '**f**' antes de las comillas de apertura y llaves para indicar dónde se insertarán las variables o expresiones.

Ejemplo:
```python
name = "Dobliuw"

print(f"\n[+] Hi my name is {name}")
```

-----


