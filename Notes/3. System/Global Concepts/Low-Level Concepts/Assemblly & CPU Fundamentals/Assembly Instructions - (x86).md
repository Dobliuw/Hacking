# Assembly

El **lenguaje ensamblador** (**Assembly language**) es un lenguaje de programación de bajo nivel que está muy cerca del lenguaje máquina, el cual es comprendido directamente por la CPU. A diferencia de los lenguajes de alto nivel como C o Python, el ensamblador proporciona control directo sobre el hardware y es específico para cada arquitectura de CPU.

Sus componentes principales se dividen en:

- **Registries**: Pequeñas unidades de almacenamiento dentro de la CPU utilizadas para realizar operaciones. Ejemplos de registros en la arquitectura x86 son `EAX`, `EBX`, `ECX` y `EDX`. Explicación de que son los registros y el uso de estos en [[CPU & Assembly Basics#Registries]]. 
- **Instructions**: Comandos que le dicen a la CPU qué operaciones realizar. Las instrucciones pueden ser de varios tipos, incluyendo aritméticas, de movimiento de datos, de control de flujo, entre otras.
- **Directives**: Las directivas son comandos que proporcionan información al ensamblador pero no se traducen directamente a instrucciones de máquina. Ejemplos incliyen `.data` para definiciar una sección de datos y `.text` para definir una sección de código.
- **Labels**: Las etiquetas son identificadores que se utilizan para marcar posiciones en el código, permitiendo saltos y llamadas a funciones.

---
# Life Cycle of Assembly Code

El ciclo de vida de un programa codeado en lenguaje ensamblador se separa en algunos puntos claves: 

1. **Source Code**
El código fuente es el programa escrito por el programador en un lenguaje de alto nivel (C, C++, Python, etc.) o en ensamblador. Este es el punto de partida.

2. **Assembly**
Continuamos con el ensamblado, momento en el que si el código fuente está en ensamblador, se utiliza un *ensamblador* (Como `as` en GNU) para convertir el código en *lenguaje máquina*. Este proceso genera un *archivo objeto* (`.o`).

```bash
as -o program.o program.s
```

- *Machine language*
El lenguaje máquian es el conjunto de instrucciones que la CPU puede ejecutar directamente. Estas instrucciones están codificadas en binario y son específicas para cada arquitectura de la CPU. El lenguaje máquina es el nivel más bajo de abstracción y consiste en secuencias de bits que representan operaciones y datos. Ejemplo: `10110000 01100001`

- *Object language*
El térmi "*lenguaje objeto*" generalmente se refiere al código objeto o archivos objeto (`.o`). Los archivos objeto son el resultado del ensamblado del código fuente (En ensamblado o en un lenaguaje de alto nivel) y contiene código máquina, pero también incluyen metadatos adicionales necesarios para la **vinculación**, como símbolos y tables de reubicación.

3. **Compilation**
Para lenguajes de alto nivel, se usa un compilador (Como `gcc` para C) que realiza dos tareas:
- *Traducción a Ensamblador*: Convierte el código fuente a código ensamblador.
- *Ensamblado Automático*: Convierte el código ensamblador a código objeto.

```bash
gcc -c program.c -o program.o
```

La flag `-c` indica que solo se quiere compilar y ensamblar, no *enlazar*. 

4. **Linking**
El proceso final, la vinculación o el enlace, toma uno o más archivos objeto y los combina en un único ejecutable, se utiliza un enlazador (`ld` en GNU) el cual resuelve las referencias a funciones y variables externas.

```bash
ld -o final_executable program.o
gcc program.o -o final_executable
```

---
# Assembly Instructions

#### Data Movement Instructions

- **mov** 

La instrucción `mov` es fundamental en el lenguaje ensamblador, utilizada ara mover datos entre registros, entre registros y memoria, o entre un registro y un valor inmediato. Si bien los movimientos de registro a registro son factibles, no se admiten movimientos directos de memoria a memoria, dado que cuando son necesaria transferencias de memoria, el contenido de la memoria de origen debe cargarse incialmente en un registro, que luego puede almacenarse en la dirección de la memoria de destino.

*Syntax*
```asm
mov {reg}, {reg}
mov {reg}, {mem}
mov {mem}, {reg}
mov {reg}, {const}
mov {mem}, {const}
```

*Example*
```asm
mov eax, ebx             ; Copy the value in ebx into eax
mov byte ptr [var], 5    ; Store the value 5 into the byte at location var
```


---
# Final Example

1. **Source code**: Archivo `hello.s`: 
```assembly
section .data
	msg db 'Hello, World!', 0

section .text
	global _start

_start:
	; Write the message to stdout
	mov eax, 4         ; sys_write = 4 
	mov ebx, 1         ; file descriptor (stdout = 1)
	mov ecx, msg       ; message to write
	mov edx, 13        ; message length
	int 0x80           ; call kernel

	; Exit the program
	mov eax, 1         ; sys_exit = 1
	xor ebx, ebx       ; exit code 0
	int 0x80           ; call kernel
```

2. **Assembly**: Ensamblamos el código en lenguaje ensamblador a archivo objeto:

```bash
as -o hello.o hello.s
```

3. **Linking**: Enlazamos el o los archivo/s objeto/s:

```bash
ld -o hello_world hello.o
```
