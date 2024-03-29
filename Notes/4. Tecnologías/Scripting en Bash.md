-----
- Tags:  #linux #basico #teoria #practica
-----
# Bash
El script en **Bash** (Bourne-Again Shell) es un intérprete de comandos de Unix/Linux que permite a los usuarios interactuar con el sistema operativo mediante comandos. Además de ser una interfaz de línea de comandos, Bash también es un lenguaje de scripting que permite la automatización de tareas y la creación de programas simples.

----
# Variables
```bash
# Asigna un valor a la variable
variable="Valor"
# Imprimir el varlo de la variable
echo $variable
# Declara una variable de read only
declare -r variable="valor"
# Declara una variable de tipo integer
declare -i variable_numerica=1
# Declara un array de datos
declare -a variable_array=("dato1" 2 "dato3")
```
# Condicionales
```bash
# Condicional If Else
if [[ "condition" ]]; then
	# code
else:
    # code
fi
# Doble condicional if 
if [[ "condition" ]] && [[ "condition2" ]]; then
  # code 
fi
# Condicional If Else alterno
[[ "condition" ]] && "True Condition" || "False condition"
```
# Bucles
```bash
# Bucle for
for i in {01..10}; do
	echo $i
done
# Bucle while
while true; do
    echo "while"
done
```
# Funciones
```bash
# Declarar una funcion
function my_function(){
	# code
}

# Ejecutar una funcion
my_function

# Pasar argumentos a la funcion
my_function $arg1
```
# Lectura de datos
```bash
# Nombre del programa 
echo $0
# Primer argumento
echo $1
# Segundo argumento
echo $2
# ............

# Lectura de flags (Ejemplo -m 'argumento' y -h )
declare -i counter=0

while getopts "m:h" arg; do
	case $arg in
		m) argumento_pasado=$OPTARG; let counter+=1;;
		h) ;;
done

if [[ $counter -eq 1 ]]; then
	# Código...
else
	# Código...
fi
```
# Listas o Arrays
```bash
# Declarar array 
declare -a my_array=(1 2 3 4)

# Mostrar una posición
echo ${my_array[2]}

# Mostrar la última posición
echo ${my_array[-1]}

# Obtener la longitud del array
echo ${#my_array[@]}

# Volcar todos los elementos
echo ${my_array[@]}

# Agragar un valor
my_array+=("new_value")

# Eliminar un valor
unset my_array[4]
my_array=(${my_array[@]})


```
# Modulos 
```bash
# Hacer uso del modulo RANDOM
echo $(($RANDOM))
```