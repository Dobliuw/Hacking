----
- Tags: #tecnologías
-----
# POO (Programación Orientada a Objetos)

La **Programación Orientada a Objetos** (**POO**) es un paradigma de programacióin que utiliza objetos y clases en su enfoque central. Es una manera de estructurar y roganizar el código que refleja cómo los desarrolladores piensan sobre el mundo real y las entidades dentro de él.

----
# Self

El uso de **self** es uno de los aspectos más fundamentales y a la vez confusos para gente nueva en la POO en Python. Este identificador es crucial para entedner c+omo Python maneja los métodos y atributos dentro de sus clases y objetos
###### Definición de Self

A nivel conceptual, **self** es una referencia al objeto actual dentro de la clase. Es el primer parámetro qeu se pasa a cualquier método de una clase Python A través de self, un método puede acceder y manipular los atributos del objeto y llamar a otros métodos dentro del mismo objeto. Es importante tener en cuenta que ya que no deja de ser un argumento, este puede recibir cualquier nombre, pero por conveción se suele encontrar como **self**. 
###### Uso de Self

Cuando se crea una nueva instancia de una clase (Objeto), Python pasa automáticamente la instancia recién creada como el primer arguemento al método **__init__** (Constructor) y a otros métodos definidos en la clase que tienen self como su primer parámetro. Esto es lo que permite que un método opere con datos específicos del objeto y no con datos de la clase en general o de otras instancias de la clase.
###### Importancia de Self

El concepto de self es importante en la POO ya que segura que los métodos y atributos se apliquen al objeto correcto. Sin self, no podríamos diferenciar entre las operaciones y datos de defirentes instancias de una clase.

------
# Clases

Las clases son los fundamentos de la POO. Actúan como plantillas para la creación de objetos y definen atributos y comportamientos que los objetos creados a partir de ellas tendrán. En Python, una clase se define con la palabra clave '**class**' y proporciona la estructura inicial para todo objeto que se derive de ella.
###### Instancias de Clase y Objetos

Un objeto es una instancia de una clase. Cada vez que se crea unobjeto, se está creadun una instancia que tiene su propio espacio de memoria y conjunto de valores para los atributos defínidos por su clase. Los objetos encapsulan datos y funciones juntos en una entidad discreta.
###### Métodos de instancia de clase

Los métodos de una instacia de clase son funciones que se definen dentro de una clase y solo pueden ser llamados por las instancias de esa clase. estos métodos son el mecanismo principal para interactuar con los objetos, permitiéndoles realizar operaciones o acciones, modifcar su estado o incluso interactuar con otros objetos.

Ejemplo:
```python
# Simple Class
class Person:
	def __init__(self, name, age):
		self.name = name
		self.age = age
	def presentation(self)
		print("Hi everyone! My name is {} and I've {} years old.".format(self.name, self.age))

dobliuw = Person("Dobliuw", 20)
dobliuw.presentation() # Hi everyone! My name is Dobliuw and I've 20 years old.
print(dobliuw.name) # Dobliuw
print(dobliuw.age) # 20
```

-----
# Métodos estáticos y métodos de clase
###### Decoradores

Los decoradores son una herramienta poderosa en Python que permite modificar el comportamiento de una función o método. Funcionan como "envoltorios", que agregan funcionalidad antes y después del método o función decorada, sin cambiar su código fuente. En POO, los decoradores son frecuentemente utilizados para agregar funcionalidades de manera dinámica a los métodos, como la sincornización de hilos, la memorización de resultados o la verificación de permisos.
###### Métodos de clase

Un método de clase es un método que está ligado a la clase y no a una instancia de la clase. Esto significa que el método puede ser llamado sobre la clase misma, ne lugar de sobre un objeto de la clase. Se definen utilizando el decorador '**@classmethod**' y su primer arguemtno es siempre una referencia a la clase, convencionalmente llamada '**cls**'. Los métodos de clase son utilzados a menudo para definir métodos "factory" que pueden crear instancias de la clase de diferentes maneras.
###### Métodos Estáticos

Los métodos estáticos, definidos con el decorador '**@staticmethod**', no reciben una referencia implícita ni a la instancia (self) ni a la clase (cls). Son básicamente como funciones regulares, pero pertenecen al espacio de nopmbres de la clase. Son útiles cuando queremos realizar alguna funcionalidad que está relacionada con la clase, pero no requiere acceder a la instancia o a los atributos de la clase.

Ejemplos:
```python
# STATIC METHOD
# Class con decoradores y métodos
class Rectangulo
	def __init__(self, ancho, alto):
		self.ancho = ancho
        self.alto = alto

# El decorador property sirve para convertir en método en una "propiedad"
    @property 
	def area(self):
        return self.ancho * self.alto

# El metodo __str__ sirve para realizar y devolver una acción determinada al intentar mostrar el objeto.
    def __str__(self):
        return f"\n[+] Propiedades del rectangulo: [Ancho: {self.ancho}, Alto: {self.alto}]\n"

# El método __eq__ sirve para realizar y devolver una acción determinada al intentar comparar dos instancias de la clase (objetos).
    def __eq__(self, other):
        return self.ancho == other.ancho and self.alto == other.alto

rect1 = Rectangulo(20, 80)
rect2 = Rectangulo(20, 80)

print(f"\n[+] El área es {rect1.area}")
print(rect1)
print("Los rectangulos son iguales") if rect1 == rect2 else print("Los rectangulos NO son iguales")

###############################################################
# CLASS METHOD
# Clase con más métodos, variables y herencia
class Book:
	# Class vars
	best_seller_limit = 5000
	IVA = 0.3

	def __init__(self, title, author, price):
		self.title = title
		self.author = author
		self.price = price

	@staticmethod
	def best_seller(sells):
		return sells > Book.best_seller_limit # Using a Class vars

# El decorador @classmethod suele usarse en casos de herencia donde pueden generarse conflictos entre operaciones o acciones que deban cambiar basandose en determinadas propiedades, variables o métodos repetidos entre las clases con cambios, en este ejemplo no sería el mismo IVA de un libro digital que uno físico.
	@classmethod
	def iva_price(cls, price):
		return price + price * cls.IVA

class DigitalBook(Book): # Nueva clase hereda métodos y propiedades de la otra
	IVA = 0.5 

first_book = Book("Hacking the World", "Dobliuw", 100)
first_book_digital = DigitalBook("Hacking the World D.V", "Dobliuw", 100)

print(Book.best_seller(6000)) # True
print("\n[+] The {} book price with IVA is {}".format(first_book.title, Book.iva_price(first_book.price)))
print("\n[+] The {} digital book prive with IVA is {}".format(first_book_digital.title, DigitalBook.iva_price(first_book_digital.price)))

#########################################################################

class Students:

    students = []
    age_limit = 18

    def __init__(self, name, age):
        self.name = name
        self.age = age

        Students.students.append({"name": name, "age": age})


    @staticmethod
    def list_students():
        print("\n[i] We've registered de following students:\n")
        for i, student in enumerate(Students.students):
            print("{}) Student {} with {} years old.".format(i + 1 , student["name"], student["age"]))
        print("\n")


    @staticmethod
    def older(age):
        return age >= Students.age_limit


    @classmethod
    def create(cls, student, age):

        if cls.older(age):
            return cls(student, age)
        else:
            return f"\n[!] {student} is a minor."

```

-----
# Herencia y Polimorfismo

La herencia y el polimorfismo son conceptos fundamentales en la POO que permiten la creación de una estructura de clase flexible y reutilizable.
###### Herencia

Es un principio de la POO que permite a una clase heredar atributos y métodos de otra clase, conocida como su clase base o superclase. La herencia facilita la reutilización de código y la creación de una jerarquía de clases. Las subclases heredan las características de la superclase, lo que permite que se especialicen o modifíquen comportamientos existentes.
###### Polimorfismo

Este concepto se refiere a la habilidad de objetos de diferentes clases de ser tratados como instancias de una clase común. El polimordismo permite que una función o método interactúe con objetos de defirentes clases y los trat como si fueran del mismo tipo, siempes y cuando compartan la misma interfaz o me´todo. Esto significa que el mismo método puede comportarse de manera diferentes en distintas clases, un concepto conocido como sobrecarga de métodos.

Ambos, la herencia y el polimordismo, son piedras angulares de la POOO y son ampliamente utilizados para diseñar sistemas que son fácilmente extensibles y mantenibles.

Ejemplo de **Herencia**: 
```python  
class Animal:
		
	def __init__(self, name):
		self.name = name

	def talk(self):
		raise NotImplementedError("The subclasses should implement this method")

class Cat(Animal):
	def talk(self):
		return f"{self.name}: ¡Miau!"

  
class Dog(Animal):
	def talk(self):
		return f"{self.name}: ¡Guau!"

  
cat = Cat("Garfield")
dog = Dog("Karin")
animal = Animal("Bro")

print(cat.talk()) # "Garfield: ¡Miau!"
print(dog.talk()) # "Karin: ¡Guau!"
print(animal.talk()) # Error
```

Ejemplo de **Polimorfismo**:
```python
class Animal:
		
	def __init__(self, name):
		self.name = name

	def talk(self):
		raise NotImplementedError("The subclasses should implement this method")


class Cat(Animal):
	def talk(self):
		super().talk() # Forzar a pasar por el método "talk" en la clase padre de la cual se hereda. (Ya que la misma fue reescribida en la clase que hereda)
		return "¡Miau!"

  
class Dog(Animal):
	def talk(self):
		return "¡Guau!"


def make_talk(obj): # Esta misma función actua diferente para diferentes clases.
	print(f"{obj.name}: {obj.talk()}")

cat = Cat("Garfield")
dog = Dog("Karin")
animal = Animal("Bro")

print(cat.talk()) # "Garfield: ¡Miau!"
print(dog.talk()) # "Karin: ¡Guau!"
print(animal.talk()) # Error
```

-----
# Encapsulamiento y métodos especiales

El encapsulamiento en la programación orientada a objetos (POO) maneja principalmente tres niveles de cisibilidad para los atributos y métodos de una clase: **públicos**, **protegidos** y **privados**. En Python, esta distinción se realiza mediante convenciones en la nomenclatura, más que a través de estrictas resticciones de acceso como en otros lenguajes.
###### Atributos públicos

Son accesibles desde cualquier parte del rpgorama y, por convención, no tienen un prefijo especial. Se espera qeu estos atributos sean parte de la interfaz permanente de la clase.

Ejemplo:
```python
class Bank:
	def __init__(self, money):
		self.money = money
```
###### Atributos protegidos

Se indiica con un único guion bajo al principio del nombre (Por ejemplo **\_atributo**). Esto es solo una convención y no impide el acceso desde fuera de la clase, pero se entiende que estos atruibutos están protefidos y no deberían ser accesibles directamente, excepto dentro de la propia clase y en subclases.

Ejemplo:
```python
class Bank:
	def __init__(self, money):
		self._money = money
```
###### Atributos privados

En Python, los atributos privados se indican con un doble guion bajo al principio del nombre (Por ejemplo, **\_\_atributo**). Esto activa un mecanismo de cambio de nombre conocido como *name mangling*, donde el i ntérprete de Python alter internamente el nombre del atributo para hacer más difícil su acceso desde fuera de la clase.

Ejemplo:
```python
class Bank:
	def __init__(self, money):
		self.__money = money

# Para acceder a los atributos:
print(self._Bank__money)
```
###### Métodos especiales

Los métodos especiales en Python son tambie´n conocidos como métodos mágicos y son identificados por doble guion bajo al inicio y al final (**__metodo__**). Permiten a las clases en Python emular el comportamiento de los tipos incorporados y responder a operadores específicos. Por ejemplo, el método **__init__** se utiliza para inciializar una nueva instancia de una clase, **__str__** se invoca para una representación en forma de cadena legible del objeto y **__len__** devuelve la longitud del objeto.

Algunos de los métodos especiales importantes en POO son:

- **__init__(self, \[....\])**: Inicializa una nueva instacia de la calse.
- **__str__(self)**: Devuelve una representación en cadena de texto de lobjeto, invocado por la función **str(obj)** y **print**.
- **__repr__(self)**: Devuelve una representación del objeto que debería, en teoría, ser una expresión válida de Python, invocado por la función **repr(obj)**.
- **__eq__(self, other)**: Define el comportamiento del operador de igualdad *\=\=*.
- **__it__(self, other)**, **__le__(self, other)**, **__gt__(self, other)**, **__ge__(self, other)**: Definene el comportamiento de los operadores de comparación (*>*, *<*, *>=* y *<=* respectivamente).
- **__add__(self, other)**, **__sub__(self, other)**, **__mul__(self, other)**, etc: Definen el comportamiento de los operadores aritméticos (*+*, *-*, *\**, etc ).

Ejemplos:
```python
class Box:
	def __init__(self, *items):
		self.items = list(items)

	def __len__(self):
		return len(self.items)

	def __getitem__(self, i):
		return self.items[i]

	def __call__(self):
		for i in self.items:
			print(f"{i})")

	def __add__(self, num):
		for i in self.items:
			num += i
		return num

box = Box(1,2,3,4,5,6,7,8,9,10)
print(len(box)) # 10
print(box[5]) # 6
box() # 1) 2) 3) 4) 5) 6) 7) 8) 9) 10)
print(box + 1) 

#######################################

class Contador:
	def __init__(self, num):
		self.limit = num
        

	def __iter__(self):
		self.count = 0
		return self

  
	def __next__(self):
		if self.count < self.limit:
			self.count += 1
			return self.count
        else:
			raise StopIteration

cincuenta = Contador(50)

for i in cincuenta:
	print(i)
```

------
# Decoradores y Propiedades