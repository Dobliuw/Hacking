--------
- Tags: #teoria #sistemas #pipes
-----
# ¿ Que es un Pipe ?

Los Pipes son un Mecanismo de Comunicación entre Procesos, más conocido como *IPC*. Un pipe es una forma de establecer una comunicación unidireccional entre dos procesos. 

Las comunicaciones Pipes utilizan la implementación **First-in-First-out** (*FIFO*).

Esto significa que el primer byte de data escrito en un pipe será el primer byte de data que será leido por el mismo. Despues de que los datos sean leídos por el pipe, ya no está disponible dentro del búfer de datos de la tubería y, por lo tanto, no se puede volver a leer.

----
# Tipo de Pipes

Existen dos principales tipos de Pipes: *Named Piepes*, los cuales son Pipes con nombre y *Anonymous Pipes*, los cuales no tienen nombre.

Un ejemplo de un *Named Pipe* puede ser aquel que utilizemos en sistemas Unix con el comanod `mkfifo`, ejemplo:

```bash
mkfifo named_pipe_example # Creación de named pipe
cat /etc/passwd > named_pipe_example # Stdout redirigido a el named pipe

more < named_pipe_example # Leyendo datos del pipe
```

De esta manera, estamos haciendo uso del comando **mkfifo** para la creación de un *named pipe*, en este caso con el nombre de *named_pipe_example*, donde posteriormente estamos enviando los datos del stdout del comando `cat /etc/passwd`, donde posteriormente desde otro procesos estamos leyendo los datos de este pipe con otro comando el cual es `more < named_pipe_example`.

Así mismo, un ejemplo de *Anonymous Pipes* / *Unnamed Pipes* es el uso cotidiano de la concatenación de comandos en sistemoas Unix, por ejemplo:

```bash
cat /etc/passwd | grep 'root' | tr ':' '>'
```

En este caso, mediante el uso de *unnamed pipes* estamos concatenando el **stdout** de un comando, para convertirlo mediante pipes en el **stdin** de otro comando y así susesivamente.

En el caso de Windows esto es un poco más avanzado y complejo. Pero recursos como [este](https://www.ired.team/offensive-security/privilege-escalation/windows-namedpipes-privilege-escalation) hablan de la explicación de Named Pipes en Windows y su explotación por parte de los atacantes.

Podríamos intentar listar todos los Pipes de Windows con el siguiente comando de PowerShell:

```powershell
# Opción 1 
$pipes = [System.IO.Directory]::GetFiles("\\.\\pipe\\")
echo $pipes

# Opción 2
Get-ChildItem \\.\pipe\
```

Mientras que en linux podríamos hacer uso de:

```bash
find / -type p 2>/dev/null
```

----

