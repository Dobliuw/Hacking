# C 

*C* es un lenguaje de programación de propósito general, este lenguaje esta orientado a la implementación de sistemas operativos, concretamente Unix.

Es importante tener en cuenta y recordar que existen lenguajes de programación **compilados** vs **interpretados**, lenguajes de programación *interpretados* como Python o JavaScript utilizan un interprete el cual ejecuta el código y en tiempo real dado que se va leyendo línea tras línea. Por otro lado lenguajes *compilados* como C utilizan un compilador (Como *gcc* o *clang*) para traducir el archivo escrito en C (file.c) a un archivo de bajo nivel.

```bash
cd C:\path\to\script\folder

gcc script.c -o final_script

.\final_script
```
# Sintaxis 

Para empezar, hay que tener en cuenta esta línea recurrente en la programación de C, empezando por **#include**, es la prefunción que utilizamos para la implementación de otros recursos en nuestro código (Librerias), como lo es *import* en lenguajes como JavaScript o Python. Siguiendo con **\<stdio.h>** tenemos que dividir esto en 3, por un lado **std** proveniente de *Standard*, por otro lado la **i**, proveniente de *Input* y por último la **o**, proveniente de *Output*, ya que esta libreria contiene funciones estándar de manejo de entradas y salidas, como leer teclado o escribir en consola.

```C
#include <stdio.h>
```

A su vez, C es un lenguaje de programación fuertemente tipado, lo que implica que a diferencia de lenguajes como JavaScript en este caso será constantemente necesario la declaración de tipo de datos que serán las variables, o devolveran las funciones, etc.

```C
#include <stdio.h>
#include <stdbool.h> // Library to work with True and False

int age = 20; // %d
float money = 3.141592; // 4 bytes (32 bits of memory) 6-7 digits (%f)
double money2 = 3.1415924324234; // 8 bytes (64 bits of memory) 15-16 digits (%lf)
bool condition = true; // 1 byte (8 bits) true -  false (%d)
char letter = 'a'; // 1 byte (Chars or nums from -128 to +127 = ASCII) %d (The num) or %c (The char)
signed char letter2 = 'a'; // 1 byte (Chars or nums from -128 to +127 = ASCII) %d (The num) or %c (The char)
unsigned char letter3 = 'a'; // 1 byte (Chars or nums from 0 to 255 = ASCII) %d (The num) or %c (The char)
char name[] = "Dobliuw"; // Array of characters %s

const float PI = 3.14159; // Keyword CONST to make a var constant.

void sayHello(){
	printf("Hey you wspp cuz!");
};

int main(){
	// .... code 
	return 0;
};

/*
This is a multiple 
line comment bdw
*/
```
##### Signed VS Unsiged

Antes de proseguir con algunos detalles a tener en cuenta en ciertos tipos de datos, es importante tener en cuenta aquellos tipos de datos que estan *signed* vs aquellos que estan *unsigned*, ya que esto cambia cómo se interpreta y representa un tipo de datos en términos de su rango de valores permitidos

- **Signed**: Un tipo de dato *signed*, como `signed char` o `signed int`, etc. puede representar tanto *valores positivos como negativos*. El bit más alto (El bit más a la izquierda) se utiliza para representar el signo del número lo que significa que un tipo de dato *signed* tiene un rango que incluye valores negativos , cero y valores positivos.
	-  Ejemplo: `signed char` tiene un rango de **-128** a **127** (1 byte = 8 bits = 2^8 = 256 d pero queda en 255 dado que 1 bit se utiliza para el signo + o -)

- **Unsigned**: Un tipo de dato *unsigned*, como `unsigned char`, `unsigned int`, etc. solo puede representar *valores no negativos* (Positivos y cero). El bit más alto se utiliza para representar un valor en lugar de un signo.
	-  Ejemplo: `unsigned char` tiene un rango de **0** a **255** (1 byte = 8 bits = 2^8 = 256 d)

##### Double float

En C, *double* es un tipo de dato utilizado para representar números con coma con mayor precisión que *float*. Mientras que *float* normlamente utiliza 4 bytes (32 bits) para almacenar números con coma, **double** utiliza *8 bytes* (64 bits), lo que proporciona más precisión y un rango más amplio de valores.
##### Char 

En C, el tipo de dato *char* se utiliza principalmente para almacenar caracteres individuales. Sin embargo, debido a la forma en que se representa internamente en la memoria, también se puede utilizar para almacenar y manipuara valores numéricos.

- Límites: En C, *char* tiene un rango de **-128** a **127** si es *signed*, de **0** a **255** si es *unsigned*. 
##### Short

En C, el tipo de dato *short* se utiliza para representar enteros cortos, es decir, números enteros que requieren menos espacio en memoria que un *int* que suele tener un total de 4 bytes (En sistemas de 32 bits) = 32 bits = 2^32 = 4.294.967.296 (Recordando que por defecto esta *signed*, permite un rango de **-2.147.483.648** a **2,147,483,647**, en caso de estar *unsigned* de **0** a **4.294.967.295**).

- Límites: En C, *short* tiene un rango de **-32.768** a **32.767** (2 bytes = 16 bits = 2^16 = 65.536 d pero quedan 65.535 dado que 1 bit se utiliza para el signo + o -).
- Si se convina con *unsigned* es decir, *unsigned short* recordemos que altera el valor pasando de **0** a **65.535** (2 bytes = 16 bits = 2^16 = 65.536)
- Short siempre tendrá un valor de 2 bytes, únicamente en caso de estar signed o unsigned cambia el signo.

En caso de sobrepasarnos el valor disponible a asignar dentro de estos rangos, se reseteara al minimo valor posible (En caso de ser *unsigned* a **-32.768** y en caso de no especificar *signed* o que lo esté, a **0**).
##### Long

En C, el tipo de dato *long* se utiliza para representar números enteros más grandes que los que puede contener *int*. Es importante tener en cuenta que *dependiendo de la arquitectura* del sistema operativo *long* tendrá un total de bytes distinto.

- Arquitectura: En sistemas operativos de 32 bits, *long* tendrá un total de *4 bytes* y un total de *8 bytes* en sistemas de 64 bits.
- Límites: En C, *long* tiene un rango de **-2.147.483.648** a **2,147,483,647** en caso de estar *signed* en OS de 32 bits y un total de **-9,223,372,036,854,775,808** a **9,223,372,036,854,775,807.** en caso de estar signed en OS de 64 bits. En caso de esta *unisgned*, *long* tiene un rango de **0** a **4,294,967,295** en sistemas de 32 bits y de **0** a **18,446,744,073,709,551,615** en sistemas de 64 bits.

Es importante tener en cuenta que en sistemas de 32 bits tanto *int* como *long int* tendran el mismo tamaño de almacenamiento (4 bytes = 32 bits) y *long long int* un tamaño de 8 bytes (64 bits) y rango de representación de datos. Mientras que en sistemas de 64 bits:

- *int* = 4 bytes = 32 bits = 2^32 = 4.294.967.296
- *long int* o *long* = 8 bytes = 64 bits = 2^64 = 18.446.744.073.709.551.616
- *long long int* =  8 bytes = 64 bits = 2^64 = 18.446.744.073.709.551.616

Basicamente, en sistemas de 32 bits los *int* y los *long int* / *long* suelen tener la misma capacidad de espacio en memoria, mientras que en sistemas de 64 bits los *long int* / *long* y los *long long int* suelen tener la misma capacidad de almacenamiento en memoria
##### Representaciones

Para representar los distintos tipos de datos haremos uso del % seguido de uno o más caracteres que hagan alución al tipo de dato que se esta intentando representar

```C
printf("%c",some_var); // Char
printf("%s",some_var); // Char array (String)
printf("%f",some_var); // Float
printf("%lf",some_var); // Double
printf("%d",some_var); // Bool
printf("%d",some_var); // Char as numeric value (ASCII)
printf("%d",some_var); // Unsigned char as numeric value (ASCII)
printf("%d",some_var); // Short
printf("%d",some_var); // Unsigned short
printf("%d",some_var); // Integer
printf("%u",some_var); // Unsigned integer
printf("%lld",some_var); // Long long integer
printf("%llu",some_var); // Unsigned long long integer
```
##### Formating

Cuando trabajamos con la función *printf* es fundamental tener conocimiento sobre el formateo de representación de datos, esto nos permite controlar cómo se muestran los datos cuando imprimimos en pantalla los mismos, especificamente detalles como el número de decimales para los números *float*, la "anchura" (*width*) de campo para los enteros, etc

```C
// For INTEGERS
%d // INT con signo (Decimal)
%i // INT con signo (Decimal)
%u // INT sin signo (Decimal)
%o // INT sin signo (Octal)
%x // INT sin signo (Hexadecimal)
%X // INT sin signo (Hexadecimal)
%{num}d // INT con {num} de espacios a la derecha
%-{num}d // INT con {num} de espacios a la izquierda

// For FLOATS
%f // FLOAT con signo (Decimal)
%e // FLOAT notación científica.
%E // FLOAT notación científica.
%g // FLOAT notación decimal o científica.
%G // FLOAT notación decimal o científica.

// Examples
short int int_var = 255;
float float_var = 4.4325432;

printf("hola%10dhola%-10dhola",int_var,int_var); // hola       255hola255       hola
printf("%.2f",float_var); // 4.43
printf("%-10.3fhola",float_var); // 4.432          hola
```
##### Strings handle

Las funciones de *strings* en C son funciones predefinidas en la biblioteca estándar **string.h** que permite realizar varias operaciones en cadenas de caracteres. 

```C
#include <stdio.h>
#include <string.h>
char str1[] = "DOBLIUW";
char str2[] = "Gvng";

// Returns a string
strlwr(str1); // dobliuw
strupr(str2); // GVNG
strcat(str1, str2); // DOBLIUWGvng
strncat(str1, str2, 2); // DOBLIUWGv
strcpy(str1, str2); // Convert str1 in str2
strncpy(str1, str2, 2) // GvBLIUW 
strset(str1, '?'); // ?????? (Replace each char for the given one)
strrev(str1); // WUILBOD

// Returns a integer
strlen(str1); // 7
strcmp(str1, str2); // Compare if the strings are equals and if it return 0 else return another number
strncmp(str1, str2, 2) // Compare the first 2 chars of the strings
strcmpi(str1, str2); // Compare if the strings are equals (Ignore case)
strnicmp(str1, str2, 2) // Compare the first 2 chars of the strings (Ignore case)
```
##### Airthmetic operators

Los operadores aritméticos en C son utilizados para realizar operaciones matemáticas básicas en variables numéricas.

```C
+ // Addtion
- // Substraction
* // Multiplication
/ // Division
% // Modulus
++ // Increment
-- // Decrement

int num1 = 5;
int num2 = 2;

int num3 = num1 / num2; // This is equal 2... why? 
float num3 = num1 / (float) num2; // This is equal 2.500000

// Augmented assignment operators
int x = 10;
x+=2; // 12
x-=2; // 10
x*=2; // 20
x/=2; // 10
x%=2; // 0
```
##### Pointers

Los punteros en C son una característica poderosa y fundamental en el lenguaje. Un puntero es una varibale que contiene la dirección de memoria de otra variable. En escencia un puntero "apunta" a la ubicación en memoria de otra variable.

- Cuando agregamos **&** delante de una variable se imprimira la dirección en memoria de dicha variable.
- Cuando modificamos un puntero *sin* el **\*** delante, modificaremos el puntero en si.
- Cuando modificamos un puntero *con* el **\*** delante, modifcaremos la variable a la que apunta el puntero.

```C
#include <stdio.h>

void main(){
	short int num1 = 10;
	printf("The 'num1' var have %d value found in %x memory direction.",num1,&num1);
	short int *short_pointer; // We create a pointer (Short int data type)
	short_pointer = &num1; // We asign the same memory direction of num1 var
	*short_pointer = 666; // We modify (With * key) the num1 var through pointer
	printf("The 'num1' var have %d value found in %x memory direction.",num1,&short_pointer);
};
```
##### Strings

En C, las cadenas de caracteres o *strings*, son secuencias de caracteres terminadas por el carácter nulo `'\0'` o *null byte*. La biblioteca estándar de C proporciona varias funciones para trabajar strings.

```C
#include <string.h>

char sentence[100] = "This is a random sentences to an example.";
printf("The length of the sentence is %d",strlen(sentence)); // strlen returns the length of the string 

sentence[strlen(sentence) - 1] = '\0'; // Add at then end of string the null byte

```
##### User input

Para obtener la entrada del usuario en C, utilizamos la función *scanf* junto con las conversiones adecuadas para el tipo de datos que queremos leer.

```C
#include <stdio.h>
#include <string.h>

short int age; 
char name[25];

printf("\nHey, what's your name cuz? ");
scanf("%s",&name); // This wouldn't add us whitespaces 
fgets(name, sizeof(name), stdin);// Instead we need use fgets
printf("\nOh ok.. and how old are u %s? ",name);
scanf("%d",&age);
printf("It's a pleasure %s with %d years olds!\n",name,age);
```
##### Math functions

La biblioteca *math.h* en C proporciona una variedad de funciones matemáticas. Estas funciones permiten realizar operaciones matemáticas avanzadas como potencias, raíces, funciones trigonométricas, logaritmos, etc.

```C
#include <math.h>

// Square root (Raíz cuadrada)
double raiz_de_veinte = sqrt(20);
printf("%.2lf",raiz_de_veinte) // 4.47
// Pow (Potencia)
double dos_a_la_dieciseis =  pow(2, 16);
printf("%.2lf",dos_a_la_dieciseis); // 65536.00
// Round (Redondear)
int cuatro_redondeado = round(4.14);
printf("%d",cuatro_redondeado); // 4
// Round Up (Redondear para arriba)
int cuatro = ceil(3.14);
printf("%d",cuatro); // 4
// Round Down (Redondear para abajo)
int tres = floor(3.99);
printf("%d",tres); // 3
// Get absolute value 
double cien = fabs(-100);
printf("%.2lf",cien); // 100.00
// Calculate natural logaritm (Calcular logaritmo natural)
double log_natural_de_5 = log(5);
printf("%.2lf",log_natural_de_5); // 1.61

// There are more functions to calculate more matematic things like cosine, tangent, sine
// https://www.programiz.com/c-programming/library-function/math.h
```

----
# Statements
##### If statement y Ternario

Es una estructura de control fundamental en la mayoría de lenguajes de rpogramación. Sirve para tomar decisiones en fundión de una condición booleana.

```C
// ..... code 
if(condition1 == true){
	// .... code
}else if(condition2 == true && num <= 10){
	// .... code
}else{
	// .... code
};
```

Por otro lado, el operador ternario, también conocido como operador condicional, es una expresión que se utiliza en algunos lenguajes de programación para tomar decisiones acortando el código a una línea de código. Es una forma concisa de llevar a cabo un *if-else*. 

```C
condition1 ? make_something_if_condition_is_true() : make_something_if_condition_is_false();
```

##### Switch statement

La devalaración *switch* en C es otra estructura de control que permite tomar decisiones basadas en el valor de una expresión o variable. Es útil cuando se tinen múltiples casos posibles y se quiere ejecutar diferentes bloques de código según el valor de la expresión.

```C
#include <stdio.h>
// .... code
char note ;
printf("How much did you get on the exam?");
scanf("%c", &note);

switch(note){
	case 'A':
		printf("OMG! Congratulations, you did it perfect!");
		break;
	case 'B':
		printf("Nice! You did good!");
		break;
	case 'C':
		printf("Well.. You did it okay.");
		break;
	case 'D':
		printf("At least it's not an F...");
		break;
	case 'F':
		printf("Sad... you failed.");
		break;
	default:
		printf("Please enter only a valid note.");
}
```
##### Function & Function Prototype

Una función es un bloque de código que realiza una tarea específica y puede ser llamada desde otras partes del programa. Las funciones ayudan a organizar el código, promueven la reutilización y facilitan la comprensión del programa al dividirlo en partes más pequeñas y manejables.

```C
#include <stdio.h>

# Declaration 
int suma(int num1, int num2){
	return sum1 + sum2;
};

# Function call
suma(4, 5);
```

Tanto para la función como para los argumentos que la misma reciba, se deberá declarar e indicar que tipo de valor se estará haciendo uso.

Por otro lado, un *function prototype*, también conocido como *declaración de función*, es una declaración que informa al compilador acerca de la existencia y la estrucutra de una función antes que se la llame o defina. Proporciona al compilador la información necesaria sobre el nombre de la función, los tipos de parámetros que recibe y el tipo de valor que devuelve la misma, para que a la hora de hacer uso de esta, en caso de cometer un error ya sea en la cantidad de argumentos, en el tipo de datos de los argumentos y lo que sea, en lugar de obtener un warning obtengamos un error.

```C
int suma(int num1, int num2);

int main(){
	// .... code
	suma(4);
};

int suma(int num1, int num2){}
	return num1 + num2;
};
```

En este caso podemos ver que estamos declarando la función en las primeras líneas, ingresando el cuerpo de la misma al final y llamandola en la función *main*, en este caso obtendremos un error gracias a que en la primera línea estamos haciendo uso de *function prototype* y estamos declarando la función y el compilador sabe a lujo y detalle sobre la misma, en caso de no tener esta primera línea, a pesar de estar llamando a la función con un único argumento, esto desembocará en un comportamiento inesperado y un único warning en lugar de un error.
##### For loop

El bucle *for* en C es una estructura de control que se utiliza para repetir un bloqeu de código un número específico de veces. Es útil cuando sabemos exactamente cuántas veces se quiere realizar una acción.

```C
# Structure
for(initialization, condition, update){
	// .... code to execute
}

# Example
for(int counter = 0; counter <= 100; counter++){
	printf("%d\n", counter);
};
# 1
# 2 
# 3
# ....
# 100
```
##### While loop

El bucle *while* evalúa la condición antes de ejecutar el bloque de código. Si la condición es verdadera, el bloque de cóidog se ejecuta; si la condición es falsa desde el principio, el bloque de código no se ejecuta en absoluto.

```C
# Strcutre
while(condition){
	// ...code
};

# Example
int age = 1;

while(age <= 18){
	printf("One more year of life! I've %d years old right now.", age);
	age++;
};
# One more year of life! I've 1 years old right now.
# One more year of life! I've 2 years old right now.
# One more year of life! I've 3 years old right now.
# ...........
# One more year of life! I've 18 years old right now.
```
##### Do-While loop

El bucle *do-while* es similar al bucle *while*, pero la condición se evalúa después de ejecutar el bloque de código al menos una vez. Esto significa que el bloque de código se ejecutará al menos una vez, incluso si la condición es falsa desde el principio.

```C
# Structure
do{
	// ...code
}while(condition);

# Example
int i = 100;
do{
	printf("%d",i);
}while(i >= 1000);
# 100
```
##### Arrays

Un array es una estructura de datos que puede almacenar una colección de elementos del mismo tipo. Los elementos de un array están dispuestos en una secuencia contigua de memoria, y cada elemento tiene una posición única dentro del array, que se indentifica mediante un índice.

```C
int numbers[] = {1,2,3,4,5,6,7,8,9,10};
double prices[5] = {10.0, 14.0, 30.0, 50.0, 5.5};

// Found the lenght:

// We now that the function SIZEOF is used to found the bytes of an array
// sizeof(numbers) = 10.... each item is INT, INT have 4 bytes, 10 itemos * 4 bytes each one = 40 bytes
// So, once knowing the bytes used, we need divide that for the bytes of each item (INT = 4 Bytes)
// 40 bytes (10 items of 4 bytes each one) / 4 bytes (INT) = 10 items

// Create a macro:

#define length(arr) (sizeof(arr) / sizeof(arr[0]))

length(numbers) // 10
```
###### 2D Arrays

Un array 2D o *array bidimensional*, comúnmente conocidcomo como **matriz**, es una estructura de datos que contiene elementos dispuestos en filas y columnas. En C, se puede pensar en una matriz como un array de arrays, donde cadad elemento del array principal es en sí mismo un array.

```C
// Strcuture
data_type array_name[rows][columns];

// Example
int matriz[3][3] = {
	{1, 2, 3},
	{4, 5, 6},
	{7, 8, 9}
};
printf("%d", matriz[1][1]); // 5 


int main(){
    short counter = 1;
    int matriz[5][5];

    for(int i = 0; i < 10; i++){
        for(int j = 0; j < 10; j++){
            matriz[i][j] = counter;
            counter++;
        };
    };

    printf("Matriz created:\n ");

    for(int i = 0; i < length(matriz); i++){
        for(int j = 0; j < length(matriz[0]); j++){
            printf("%d ",matriz[i][j]);
        };
        printf("\n");
    };
};
```

Este concepto es el utilizado para poder dar lugar al conocido array de strings en C.

```C
// Declaration
char string_arr[][10] = {"Dobliuw", "ZaikoARG", "Elswix"};

// Change values
#include <string.h>
strcpy(string_arr[2], "ElswixGOD");
```
##### Intercambiar datos de una variable

El hecho de intercambiar valores de una variable a otra puede ser una técnica que utilizemos cotidianamente al hacer uso de arrays en C.

```C
#include <string.h>

char x[] = 'Water';
char y[] = 'Limonade';
char temp[15];

strcpy(temp, x);
strcpy(x, y); // If y have less bytes that x, that would throw and unexpected behavior
strcpy(y, temp);

int array[] = {1,2,3,4,5,6,7,8,9,10};
int size = sizeof(array) / sizeof(array[0])
```

Un ejemplo de caso de uso sería para el famoso *buble sort* para ordenar arrays de manera creciente o decreciente:

```C
#include <stdio.h>
#include <stdbool.h>
#define get_length(arr) (sizeof(array) / sizeof(array[0]))

void printArr(int arr[], int size, bool n);

int bubleSort(int arr[], int size){
    int temp;
    printf("Array pre sort: ");
    printArr(arr, size, false);
    for(int i=0; i < size - 1; i++){
        printf("\n[!] Checking %d",arr[i]);
        for(int j=0; j < size - i - 1; j++){
            printf("\n\t+ Checking %d and %d",arr[j],arr[j+1]);
            if(arr[j] < arr[j+1]){
                printf("\n\t\t[i] Swap %d for %d",arr[j],arr[j+1]);
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            };
        };
        printArr(arr, size, true);
    };
};
 
void printArr(int arr[], int size, bool n){
    n ? printf("\n\n") : (void)0;
    for(int i = 0; i < size; i++){
        printf("%d ", arr[i]);
    };
    n ? printf("\n") : (void)0;
};

int main() {
    int array[] = {4,253,14,45,26,17,81,19,110};
    int length = get_length(array);
    bubleSort(array, length);
    printf("\n[+] Array buble sorted:");
    printArr(array, length, false);
};
```
##### Structs

Los *structs* en C son una forma de definir un nuevo tipo de datos que puede contener múltiples variables de diferentes tipos. Un struct puede considerarse como una "estructura" de datos qeu agrupa varios elementos relacionados juntos bajo un solo nombre. Se suele decir que este tipo de datos es muy similar a las *Clases* en lenguajes de otros lenguajes de programación, pero sin la capacidad de contener métodos.

```C
# Struct declaration
struct Person{
	char name[20];
	int age;
};

# Struct var declaration and asignation
struct Person first_person = {"Dobliuw", 20};
struct Person second_person;

# Access to the members (Atributes in other languages)
printf("The name of the person is %s and have %d years old",first_person.name, first_person.age);

# Asign values to the members of struct
strcpy(second_person.name, "Valentino");
second_person.age = 21; 
```
##### Typedef

La palabra reservada *typedef* en C se utiliza para crear alias o nombres alternativos aara tipos de datos existentes. Esto puede hacer qeu el código sea más legible y fácil de mantener, especialmente cuando se trabaja con tipos de datos largos o complejos.

```C
# Declaration of alias
#define rows_matriz2x5 2
#define columns_matriz2x5 5
typedef int Matriz2x5[rows_matriz2x5][columns_matriz2x5];

# Using the alias
Matriz2x5 my_first_matriz = {{1,2,3,4,5},{6,7,8,9,10}};

typedef int Entero;
typedef char String_25b[25];

Entero number = 1;
String_25b name = "Dobliuw";

# String array
# Example using typedef of typdef
typedef String_25b String_arr_25x5b[5];
# Example using typdef
typedef char String_arr_15x5b[25][5];

String_arr_25bx5 my_string_arr = {"Dobliuw", "ZaikoARG", "elswix", "Valentino", "Brian"};

```