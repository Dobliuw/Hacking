# Cisco IOS

Los sistemas operativos de red son similares al sistema operativo de una PC. Mediante una *GUI* (*Grafical User Interface*), un sistema operativo permite que el usuario realice acciones básicas como utilizar el mouse para hacer selecciones y ejecución de programas, introducir textos y comandos, así como ver los resultados en el monitor.

Pero como sabemos, todos los sitemas operativos estan basados en la *CLI* (*Command Line Interface*), el sistema operativo de dispositivos intermedios de Cisco no son la excepción. El *Cisco IOS* en un swtich o router, permite que un técnico de red realice lo siguiente:

- Ejecución de programas de red basados en la CLI.
- Introducción de comandos basados en texto.
- Ver resultados en el monitor.

Los dispositivos de red de Cisco ejecutan versiones epeciales de Cisco IOS. La versión de IOS dependerá del tipo de dispositivo que se utilizará y de las características necesarias. Si bien todos los dispositivos traeran un IOS y un conjutno de características predeterminados, es posible actualizar el conjunto de estas o la versión de IOS para obtener capacidades adicionales.

------
# Access methods

Los *métodos de acceso* a una consola de un dispositivo intermedio como un Switch o un Router es mediante una de las siguientes opciones:

- **Terminal**: Este es un puerto de administración físico que proporciona acceso fuera de banda a un dispositivo de Cisco. El acceso fuera de banda hace referencia al acceso por un canal de adminitración exclusivo que se usa únicamente con fines de mantenimiento del dispositivo. La ventaja de usar este tipo de conexión, mediante un cable que conecta al puerto de consola del dispositivo, es que el mismo será accesible incluso no hayan configurados servicios de redes.

- **Secure Shell** (**SSH**): Otro método para disponer de una terminal del dispositivo, es decir, establecer una sesión de CLI de manera remota a través de una interfaz virtual, es hacer uso del protocolo SSH el cual nos brindará de manera remota una conexión al dispositivo el cual podremos manejar con una términal, siendo todo el tráfico de red utilizado por este, cifrado.

- **Telnet**: Otro método, pero esta vez *inseguro*, para establecer una sesión de CLI de manera remota a través de una interfaz virtual por medio de una red, es hacer uso del protocolo Telnet. A diferencia de SSH, telnet no proporciona una conexión segura ya que todo el tráfico de red viaja en ASCII (Texto plano), sin sufrir ningún tipo de cifrado para evitar snifeos de conexión.

Adicionalmente, algunos de estos dispositivos intermedios, como los routers, pueden admitir un puerto heredado auxililar utilizado para establecer una sesión CLI de forma remota a través de una conexión telegónica utilizando un módem.

----
# Cisco IOS usage

Al igual que muchos sistemas operativos, Cisco IOS tiene su propio modo de uso, comandos y niveles de privilegio. Como característica de seguridad, el software de IOS de Cisco divide el acceso de administración en dos modos de comando:

- **Command exection mode** (**Modo de ejecución de comando**): Este modo de ejecución tiene las capacidades limitadas per resulta útil en el caso de alguna operación básica. Permite solo una cantidad limitada de comadnos de monitoreo básicos, per no permite la ejecución de ningún comando que podría cambiar la configuración del dispositivo. El *modo EXEC del usuario* se puede reconocer con la aparición del carácter '`>`' en el prompt.

- **Privileged execution mode** (**Modo de ejecución privilegiado**): Este modo de ejecución permite ejecutar comandos de configuración más todos los comandos posibles a ejecutar en el *modo EXEC del usuario*. Un administrador de redes debe acceder al *modo EXEC con privilegios* (O también llamado *modo enable*). Solo se puede ingresar al modo de configuración global y a los mmodos de configuración más altos por medio de este modo. El modo EXEC con privilegios se puede reconocer por la aparición del carácter '`#`' en el prompt.

- Cambiar al modo *EXEC privilegiado* con el comando `enable`:
```txt
Switch> enable
Switch#
```

- Cambiar al modo *EXEC de usuario* con el comando `disable`:
```txt
Switch# disable
Switch>
```

Con el comando `?` obtendremos un uso similar al del comando `help`, podremos ver opciones de comandos, comandos, ayuda de uso de un comando, etc. 

---
# Configuration and subconfiguration modes

Para configurar el dispositivo intermedio, el usuario debe ingresar al modo de configuración global, que normalmente se denomina modo de `config`. 

Desde el modo de configuración global, se realizan cambios en la configuración de la CLI qeu afectan la operación del dispositivo en su totalidad. El modod de configración global se identifica mediante un mensaje que termina con el apartado `(config)#` despues del hostname del dispositivo.

Antes de acceder a otros modos de configuración específicos, se accede al modo de configuración global. Desde este modo, el usuario puede recien ingresar a diferentes modos de *subconfiguración*. Cada uno de estos submodos permiten la configuración de una parte o función específica del dispositivo. Por ejemplo, dos modos de subconfiguración incluyen los siguientes:

- **Line mode configuration**: Se utiliza para configurar la consola, SSH, Telnet o acceso auxiliar. (Identificado con `(config-line)#` luego del hostname).
- **Interface mode configuration**: Se utiliza para configurar un puerto de swtich o una interfaz de red de router. (Identificado con `(config-if)#` luego del hostname).

- Entrar al modo de *configuración global* con el comando`configure terminal`:
```txt
Switch# configure terminal
Switch(config)#
```

Para pasar de cualquier modo de subconfiguración a un modo anterior, podremos hacer uso del comando `exit`. 
Para salir de todos los niveles de subconfiguración y retornar al modo EXEC privilegiad, podremos hacer uso del comando `end` o de la pulsación de teclas `Ctrl + z`.

- Entrar al modo de *subconfiguración de línea* con el comando `line {type_line} {number}`:
```txt
Switch(config)# line console 0
Switch(config-line)#
```

- Entrar al modo de *subconfiguración de interfaces* con el comando `interface {type_interface} {number}`:
```txt
Switch(config)# interface FastEthernet 0/1
Switch(config-if)#
```

Es importante saber que podemos trasladarnos directamente de un modo de subconfiguración a otro y no es necesario retornar al modo de configuración global.

----
# Basic configurations

Una de las primeras configuraciones que llevamos a cabo a la hora de comenzar a configurar un dispositivo es darle el nombre de host con el comando `hostname`:

```txt
Switch# configure terminal
Switch(config)# hostname Sw-Dobliuw
Sw-Dobliuw(config)#
```

Por otro lado, como sabemos, el uso de contraseñas para proteger los distintos modos EXEC son fundamentales, para esto usaremos distintos comandos como `password {password}` y `login` para habilitar el *acceso EXEC de usuario* con el comando:

```txt
Sw-Dobliuw# configure terminal
Sw-Dobliuw(config)# line console 0
Sw-Dobliuw(config-line)# password dobliuw123
Sw-Dobliuw(config-line)# login
Sw-Dobliuw(config-line)# end
Sw-Dobliuw#
```

Una vez ejecutado estos comandos, el acceso a la consola requerirá una contraseña antes de permitir el acceso. Estos comandos pueden ser llevados a cabo con VTY es pecificas, por ejemplo, para configurar las 16 VTYs posibles en un dispositivo intermedio, podriamos utilizar los comandos:

```txt
Sw-Dobliuw# configure terminal
Sw-Dobliuw(config)# line vty 0 15
Sw-Dobliuw(config-line)# password dobliuwvty123
Sw-Dobliuw(config-line)# login
Sw-Dobliuw(config-line)# {Ctrl + Z}
Sw-Dobliuw#
```

Por otro lado, para proteger con credenciales el *acceso EXEC privilegiado* utilizaremos el comando `enable secret {password}`:

```txt
Sw-Dobliuw# configure terminal
Sw-Dobliuw(config)# enable secret 123dobliuw
Sw-Dobliuw(config)# exit
Sw-Dobliuw#
```

Ahora bien.... todas estas configuraciones llevadas a cabo, se almacenarán en diferentes archivos los cuales son:

- **startup-config**: Este es el archivo de configuración guardado que se almacenará en *NVRAM*. Contiene todos los comandos que usará el dispositivo al iniciar o reinciar. Flash no pierde su contenido cuando el dispositivo está apagado.
- **running-config**: Este archivo se almacena en la memoria de acceso aleatorio (*RAM*) del dispositivo. Refleja la configuración actual. La modificación de una configuración en ejecución afecta el funcionamiento del dispositivo Cisco de inmediato. La memoria RAM es volátil, lo que indic que se perderá todo el cotenido cuando el dispositivo se apague o reinicie.

En estos archivos de configuracion podremos encontrar las credenciales utilizadas a la hora de las distintas configuraciones de seguridad tanto para el modo EXEC de usuario como para el modo EXEC privilegiado, por lo cual como deducimos, esto es una amenaza de seguridad porque cualquier que logre acceder a estos archivos obtendría las credenciales utilizadas en texto plano.

```txt
Sw-Dobliuw# show running-config
......
!
(Output omitted)
!
line con 0
password dobliuw123
login
!
.....
```

Para solucionar esto y encriptar todas las contraseñas almacenadas en ASCII, utilizaremos el comando `service password-encryption` en modo de configuración global:

```txt
Sw-Dobliuw# configure terminal
Sw-Dobliuw(config)# service password-encryption
Sw-Dobliuw(config)# exit
Sw-Dobliuw# show running-config
......
!
(Output omitted)
!
line con 0
 password 5 $l$mERr$LE36kP4e/aQWqlFEGOSh60
 login
!
.....
```

Adicionalmente podremos configurar el *banner de aviso* que podremos utilizar para mantener al personal no autorizado fuera de la red, o al menos intentar, dado que esto es uan parte importante en los procesos legales en el caso de una demanda por acceso no autorizado a un dispositivo. Es fundamental que haya un mensaje que advierta del acceso no autorizado para evitar una posible defensa exitosa dado que el dispositivo "no indicaba que el acceso para personal no autorizado no estaba permitido".

Esto lo haremos con el comando `banner motd`:

```txt
Sw-Dobliuw# configure terminal
Sw-Dobliuw(config)# banner motd #Authorized personal access only!#
```

De esta manera, a la hora de querer iniciar sesión veremos el siguiente mensaje:

```txt
Press RETURN to get started.




Authorized personal access only!

User Access Verification

Password:
```

Como mencionamos anteriormente, existen dos archivos de configuración, **startup-config** que almacena la configuración en *NVRAM* y **running-config** que almacena la configuración en *RAM*. 

Si los cambios realizados en la configuración en ejecución no tienen el efecto que buscamos y la ocnfiguración en ejecución aún no se ha guardado, podemos restaurar el dispositivo a su configuración anterior. Podríamos eliminar los comandos modificados individualmente o volver a cargar el dispositivo con el comando `reload` en modo *enable mode* para restaurar el **startup-config**.

La desventaja de usar este comando para eliminar una configuración en ejecución no guardada es la breve cantidad de tiempo que el dispositivo estará fuera de línea, causando un periodo de inactividad en la red.

Por otro lado, si los cambios no deseados se guardaron en la configuración de inicio (**startup-config**), puede ser necesario borrar todas las configuraciones. Esto requiere borrar la configuración de inicio y reinicar el dispositivo. La configuración de inicio se elimina mediante el comando `erase startup-config` estand en *enamble mode*.

Finalmente, para guardar la configuración actual (**running-config**) de manera permanente (**startup-config**) haremos uso del comando `copy running-config startup-config`. 

----
# Virtual Interface configuration in Switch

Para acceder al switch de manera remota, se deben configurar una dirección IP y una máscara de subred en la SVI (Switch Virtual Interface). Para configurar una SVI en una switch, utilice el comando `interface vlan 1` configuración global. La VLAN 1 no es una interfaz física real, sino una virtual. A continuación, agregaremos una dirección IPv4 mediante el comando `ip address {ip_address} {subnet_mask}` de la configuración de interfaz. Finalmente, habilitaremos la interfaz virtual utilizando el comando `no shutdown`.

```txt
Sw-Dobliuw# configure terminal
Sw-Dobliuw(config)# interface vlan 1
Sw-Dobliuw(config-if)# ip address 192.168.1.2 255.255.255.0
Sw-Dobliuw(config-if)# no shutdown
Sw-Dobliuw(config-if)# exit
Sw-Dobliuw(config)# ip default-gateway 192.168.1.1
```

Una vez ejecutado estos comandos, el switch dispondrá de todos los elementos IPv4 para llevar a cabo la comunicación a través de la red. Para visualizar las configuraciones de direcciones IP podremos hacer uso del comando `show ip interface brief`:

```txt
Sw-Dobliuw# show ip interface brief
Interface            IP-Address             OK? Method Status                 Protocol
FastEthernet0/1      unnasigned             YES manual down                   down
.................
.................
Vlan1                192.168.1.2            YES manual up                     down
```