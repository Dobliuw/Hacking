----
- Tags: #escalada #teoria #practica 
---

# Secuestro de la biblioteca de objetos compartidos enlazados dinámica mente

### Las **bibliotecas compartidas** son archivos que contiene funciones y recursos utilizados por múltiples programas. Cuando un programa requiere una función de una biblioteca compartida, el sistema operativo busca la biblioteca y enlaza dinámica mente la función requerida durante la ejecución del programa. Sin embargo, si el sistema no encuentra la biblioteca en las rutas predeterminadas, puede buscarla en otros directorios. 

### Un atacante puede aprovechar esta situación creando una **biblioteca compartida maliciosa** con el mismo nombre que la biblioteca legítima y colocándola en un directorio donde el sistema la buscará. Cuando el programa intenta cargar la biblioteca, el sistema cargara la versión malicioso en lugar de la legítima, permitiendo al atacante ejecutar código malicioso con los privilegios del programa víctima. 