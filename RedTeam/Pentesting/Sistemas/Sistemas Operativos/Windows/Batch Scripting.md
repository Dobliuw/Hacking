-----
- Tags: #scripting #windows #basico #teoria #practica
-----
# Batch 
**Batch** es un lenguaje de scriting utilizado en sistemas Windows para realizar tareas de automatización y ejecutar secuencias de comandos en el entorno del símbolo de sistema de Windows (cmd.exe). Los archivos de sceuncias de comandos de Batch tienen una extensión **.bat** o **.cmd**.

------
# Basic Commands
```bash
/? # Si se agrega al final de un comando, se lista el panel de ayuda
ver # Version
assoc # Extensiones con tipo de archivo
cd # Change Directory
cls # Limpiar pantalla
copy # Copiar archivo
del # Eliminar archivos
dir # Listar contenido del directorio
date # Muestra la fecha actual y la permite configurar
echo # Muesta el input como output
exit # Mata la consola
md # Make Directory
move # Mueve archivos o directorios entre directorios
path # Muestra la variable del path
pause # Frena la ejecución y espera la interacción del usuario
prompt # Cambiar simbolo del sistema
rd # Remove Directory 
ren # Rename
rem # comentarios
start # COmienza un programa en una nueva ventana o abre un documento
time # Muestra la hora
type # Muestra el contenido de un archivo
vol # Muestra la etchoiqueta del volumen del disco  el número de serie
attrib # Muestra o cambia los atributos de un archivo 
icacls # Gestion de permisos
chkdsk # Verifica el disco
choice # Brinda la validación de SI o NO al usuario 
cmd # Invoca otra instancia de cmd
comp # Compara dos archivos basandose en el tamaño
convert # Converte un volumen FAT a NTFS
driverquery # Muestra los controladores de dispositivos (drivers)
expand # Expande uno o varios archivos comprimidos
find # Filtra por palabras en archivos
format # Formatea un disco para ser usado con Windows
help # Muestra la lista de los comandos en Windows
ipconfig # Muestra la configuración de IP de windows
label # Añade, cambia o remueve etiquetas de discos
more # Listar el contenido de un archivo en formato more
net # Gestionar y consultar aspectors de la red y el sistema
ping # Tramitar una traza ICMP
shutdown # Apaga el equipo, cierra la sesión, etc.
sort # Ordena alfabeticamente el contenido
subst # Asocia una ruta de acceso a una letra de unidad
systeminfo # Muestra la configuración del sistema y el equipo
taskkill # Termina una o más tareas 
tasklist # Lista las tareas inlcuyendo el nombre y el PID
xcopy # Copia archivos o directorios de una manera más avanzada
tree # Lista el contenido en forma de arbol de manera recursiva
fc # Lista las diferencias entre dos archivos
diskpart # Muestra y configura las propiedades de una partición de disco
title # Cambia el titulo mostrado en la consola 
set # Muestra la lista de las variables de entorno
> # Redirigir output
```
# Variables
```bash
# Declarar una variable 
set variable="value"

# Declarar una variable de tipo integer
set /A variable_num=53

# Imprimir una variable 
echo %variable%

# Obtener argumentos pasados en la línea de comandos
echo %1 # Primer arg
echo %2 # Segundo arg
# .....

# GLOBAL vs LOCAL
set var1 = "test"
SETLOCAL
set var1 = "test"
ENDLOCAL
# Variable GLOBAL disponible en todo el script, LOCAL dentro del bloque de SETLOCAL - ENDLOCAL

# Si se usa choice, para leer la respuesta 
%errorlevel%

# Comentar 
Rem comentario
:: comentario
```
# Condicionales
```bash
if "condition" (
	# code
) else if "condition" (
	# code
) else (
    # code
)

# Condicionadores
equ # Equal
neq # Not equal
lss # Less than
leq # less tan or equal
gtr # Greater than 
geq # Greater than or equal
```
# Bucles
```bash
for /l %%i in ("initial","iteration","final"); do (
	echo %%i
)
```
# Funciones
```bash
# Declarar función
:function_name
# code
exit /b 0

# Invocar función
call :{function_name} {arg1,arg2,arg3}
exit /b %errorlevel%

# Example
@echo off
call :ScriptOwner dobliuw
exit /b %errorlevel%

:ScriptOwner
echo This is %~1 script
exit /b 0
```
# Arrays o Listas
```bash
# Declarar un array
set list=1 2 3 4

# Recorrer el array
(for %%i in (%list%); do (
	echo %%i
)

# Acceder a la posición de un array
echo %list[0]%

# Setear valor en una posición del array
set a[0]=1
```
# Ejemplos:
```bash
# Script que crea 10 carpetas con el format Hacked1 en una ruta que se le pasa como argumento al ejecutar el archivo
# Ejecución    file.bat C:\Users\dobliuw\Desktop
@echo off

call :CreateTenDirsInPath %1

exit /b %errorlevel%

:CreateTenDirsInPath
set path=%~1
for /l %%i in (0,1,10); do (
	md %path%\Hacked%%i
)
dir path > C:\Users\patri\Desktop\hacked.txt
exit /b 0

# Script encargado de borrar las carpetas que contengan la palabra 'hacked'
@echo off

call :DellAll %1
exit /b %errorlevel%

:DellAll
for /f %%i in ('dir /b %1 ^| findstr /i hacked') do (
	rd %%i
)
exit /b 0 
```