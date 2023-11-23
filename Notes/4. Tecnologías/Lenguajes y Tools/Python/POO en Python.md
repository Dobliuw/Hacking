----
- Tags: #tecnologías
-----
# POO (Programación Orientada a Objetos)

La **Programación Orientada a Objetos** (**POO**) es un paradigma de programacióin que utiliza objetos y clases en su enfoque central. Es una manera de estructurar y roganizar el código que refleja cómo los desarrolladores piensan sobre el mundo real y las entidades dentro de él.

----
# Clases

Las clases son los fundamentos de la POO. Actúan como lantillas para la creación de objetos y definen atributos y comportamientos que los objetos creados a partir de ellas tendrán. En Python, una clase se define con la palabra clave '**class**' y proporciona la estructura inicial para todo objeto que se derive de ella.
###### Instancias de Clase y Objetos

Un objeto es una instancia de una clase. Cada vez que se crea unobjeto, se está creadun una instancia que tiene su propio espacio de memoria y conjunto de valores para los atributos defínidos por su clase. Los objetos encapsulan datos y funciones juntos en una entidad discreta.
###### Métodos de instancia de clase

Los métodos de una instacia de clase son funciones que se definen dentro de una clase y solo pueden ser llamados por las instancias de esa clase. estos métodos son el mecanismo principal para interactuar con los objetos, permitiéndoles realizar operaciones o acciones, modifcar su estado o incluso interactuar con otros objetos.
###### Decoradores

Los decoradores son una herramienta poderosa en Python que permite modificar el comportamiento de una función o método. Funcionan como "envoltorios", que agregan funcionalidad antes y después del método o función decorada, sin cambiar su código fuente. En POO, los decoradores son frecuentemente utilizados para agregar funcionalidades de manera dinámica a los métodos, como la sincornización de hilos, la memorización de resultados o la verificación de permisos.
###### Métodos de clase

Un método de clase es un método que está ligado a la clase y no a una instancia de la clase. Esto significa que el método puede ser llamado sobre la clase misma, ne lugar de sobre un objeto de la clase. Se definen utilizando el decorador '**@classmethod**' y su primer arguemtno es siempre una referencia a la clase, convencionalmente llamada '**cls**'. Los métodos de clase son utilzados a menudo para definir métodos "factory" que pueden crear instancias de la clase de diferentes maneras.
###### Métodos Estáticos

Los métodos estáticos, definidos con el decorador '**@staticmethod**', no reciben una referencia implícita ni a la instancia (self) ni a la clase (cls). Son básicamente como funciones regulares, pero pertenecen al espacio de nopmbres de la clase. Son útiles cuando queremos realizar alguna funcionalidad que está relacionada con la clase, pero no requiere acceder a la instancia o a los atributos de la clase.

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

###############################################################

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

```