----
- Tags: #tecnologías
-----
# Expresiones regulares

Una expresión regular es una secuencia de caracteres que conforman un patrón de búsqueda. Se utilizan principalmente para la búsqueda de patrones de cadenas de caracteres u operaciones de sustituciones.

-----
# Module **re**

La librería **re** en Python proporciona un conjunto completo de herramientas para trabajar con expresiones regulares, que son patrones de cadenas diseñados para la búsqueda y manipulación de texto.

- **Funciones básicas**: *re* incluye funciones como **search** (Para buscar un patrón dentro de una cadena), **match** (Para verificar si una cadena comienza con un patrón específico), **findall** (Para encontrar todas las ocurrencias de un patrón), y **sub** (Para reemplazar partes de una cadena que coinciden con un patrón).
- **Compilación de Patrones**: Permite compilar expresiones regualres en obhjetos de patrón, lo que puede mejorar el rendimiento cuando se usan repetidamente.
- **Grupos y captura**: Ofrece la capacidad de definir grupos dentro de patrones de expresiones regulares, lo que facilita extraer partes específicas de una cadena que coinciden con subpatrones.
- **Flags**: Soporta modificadores que alteran la forma en que las expresiones regualres son interpretadas y coincididas, como ignorar mayúsculas y minúsuculas o permitir el modo multilínea.
- **Patrones complejos**: Permite la creación de patrones complejos utilizando uan variedad de símbolos y secuencias especiales, como cuantificadores, aserciones y clases de caracteres.
- **Aplicaciones prácticias**: Las expresiones regualres son extremadamente útiles en tareas como la validación de formatos (Por ejemplo, direcciones de correo electrónico), el análisis de registros (Logs), el procesamiento de lenguaje natural, y la limpieza y preparación de datos.
- **Curva de aprendizaje**: Aunque potentes, las expresiones regulares pueden ser complejas y requieren una cueva de aprendizaje. Sin embargo, una vez dominadas, se convierten en una herramienta invaluable en el arsenal de cualquier programador. 

```python
import re 

text = "This is an example test for test regex"
text2 = "This is another example. Today is 13/12/2023 and tomorrow will be 14/12/2023"
text3 = "The users can be contact with us to dobliuw@dobliuw.com or dobliuw@gmail.com"
text4 = "Field1,Field2,Field3,Field4,Field5"
text5 = "car , cart, masticart, magicarp"

test_matches = re.findall("test", text) # ['test', 'test']
dates_matches = re.findall("\d{2}\/\d{2}\/\d{4}", text2) # ['13/12/2023', '14/12/2023']
mails_groups_matches = re.findall("(\w+)@(\w+\.\w{2,})", text3) # [('dobliuw','dobliuw.com'), ('dobliuw', 'gmail.com')]
fields_matches = re.split(',', text4) # ["Field1", "Field2", "Field3", "Field4", "Field5"]
re.sub("test", "dobliuw", text) # This is an example dobliuw for dobliuw regex
re.findall(r"\bcar", text5 ) # Que empieze con car
re.findall(r"car\b", text5 ) # Que finalize con car
re.findall(r"\bcar\b", text5 ) # Que sea car 

def validate_mail(mail):
	return "Mail valid." if re.findall("[A-Za-z0-9._+-]+@[A-Za-z0-9]+\.\w{2,}", mail) else "Mail invalid."

for match in re.finditer("\d{2}\/\d{2}\/\d{4}", text2):
	print(f"La fecha {match.group(0)} empieza en la posición {match.start()} y finaliza en la posición {match.end()}")

```