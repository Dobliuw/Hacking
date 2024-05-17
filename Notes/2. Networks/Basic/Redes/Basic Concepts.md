----
- Tags: #redes #basico #teoria 
----
# Redes

Una red permite a dos computadores comunicarse entre si. Existe una amplia gama de **topologias** (mesh / tree / star), **medios** (ethernet / fiber / coax / wireless) y **protocolos** ( TCP / UDP / IPX) que pueden ser utilizados para facilitar las conexiones. 

![[basic_connection.png]]

Todo *internet* esta basado en muchas redes subdivididas, por ejemplo, en esta imagen tenemos por un lado la **Home Network** y por otro la **Company Network**. Supongamos que queremos visitar el servicio web de la compañia (Alojado en **Company Network**) desde nuestra red **Home Network**, nosotros sabemos la dirección del servicio web o más conocido como **Uniform Resource Locator** (*URL*) que ingresamos en nuestro navegador, también conocido como **Fully Qualified Domain Name** (*FQDM*).

- **URL** (https://www.hackthebox.eu/resource?query=xdata): puede contener parametros que determinen una parte especifica de la página web.
- **FQDN** (www.hackthebox.eu): solo especifica la página web.

En este simple ejemplo, la conexión comenzaria desde nuestro dispositivo localizado en **Home Network** el cual trámita una petición al servicio web de la compañia mediante nuestro router, el cual se conecta con nuestro **ISP** (Proveedor de serivcio de internet), el cual a su vez nos permite conectarnos a internet para realizar una petición a un servidor **DNS**, quien resuelve la *url* de la página web de la compañia solicitada a una *dirección IP*, la cual finalmente se utiliza para enviar nuestra petición a la máquina que hostea dicha página web. Una vez recibida la petición, la máquina que hostea la página web de la compañia hace uso del router de la **Company Network** para conectarse a su **ISP** y devolvernos la petición previamente realizada.

-----
## Direcciones *IP*:

La direcciones IP son identificadores numéricos únicos que se utilizan para identificar dispositivos en una red, como pc's, routers, servidores y otros dispositivos. Existen dos versiones (v4 y v6).
#### IPV4
 
Consiste en un formato de dirección de 32 bits y es la más utilizada, se le suele llamar "Octeto" a las unidades compuestas por 8 bits por lo que IPv4 consta de un total de 4 obtetos, ya que consta de 4 pares de 8 bits (32 en total). 

Para ver los bits del primer octeto, es decir, representaod en numeros binarios el primer número antes del punto de la ip podriamos jugando con el comando: 

```Shell
echo "$(echo "obase=2; 192" | bc).168.1.38"
```

 Ahora.... si tenemos en cuenta que hay 32 bits por cada IP, cual seria la cantidad de posibilidades de combinaciones unicas y diferentes de las demás?  Esto lo podriamos ver con el comando: 
 
```Shell
echo "2^32" | bc
```

Lo que nos devuelve "4294967296" , por lo que teniendo en cuenta que en el mundo hay 8.000.000.000+ personas, nos estamos quedando sin direcciones IPv4, por lo que se esta implementando las direcciones IPv6 con un formato asi: *"2802:8010:4928:8e01:539b:104:abc6:2c7c"*, por lo que si vieramos la cantidad de posiblidades con `echo "2^128" | bc` veriamos un total de posibilidades unicas de "340282366920938463463374607431768211456" lo que resuelve el problema y deja casi anulada la posibilidad de quedarnos sin IP's.

#### IPv6

 Tambien conocida como IPng (Next Generation Internet Protocol), ha sido diseñada para solucionar el problema de asignacion de IP's limitada y para remplazar de forma gradual a las IPv4. Consta en un  formato de dirección de 128 bits, siendo 8 grupos de dígitos *hexadecimales*,  siendo a su vez cada uno de estos 8 grupos 2 octetos cada uno (16 bits), separados en este caso por un ":".  

Ejemplo de IPv6 `2802:8010:4928:8e01:539b:104:abc6:2c7c`. 

---
## Direcciones *MAC*: 

La dirección *MAC* o dirección fisica, es un número en *hexadecimal* de 12 dígitos (Número binario de 6 bytes, es decir, 6 bloques de 8 bits), teniendo asi, la dirección *MAC* un total de 48 bits.  Esta dirección se utiliza para representar de manera "unica" cada dispositivo, una especie de DNI. En este caso hablamos de "unica" ya que existen herramientas como *macchanger* que te permiten alterar la misma. 

La *MAC* consta de, en primer lugar (Los primeros 3 octetos), representan al *OUI (Identificador Único Organizacional)*, es decir, que los 3 primeros octetos hacen alución a un número que identifica el fabricante del dispositivo, mientras que los ultimos 3 octetos representan al *NIC (Network Interface Controler Especific) o  Modelo del dispositivo*.

---
## TCP vs UDP:

El protocolo **TCP**, es un protocolo orientado a dirección, es uno de los principales protocolos en redes TPC/IP, proporciona verificación de errores y se comprueba que los datos se hayan entregado, es decir, proporciona una entrega de datos confiable, mientras que **UDP** es un protocolo NO orientado a la conexión el cual manda constantemente datos sin verificar la integridad ni el recibimiento de los mismos, es decir NO garantiza la entrega de datos.  

Cuando hablamos del protocolo *TCP* es importante tener en cuenta una parte crucial de este, el cual es *Three-Way Handshake*, un procedimiento utilizado para establecer una conexión entre dos dispositivos. Este procedimiento consta de tres pasos 1. *SYN*, 2. *SYN-ACK*, 3. *ACK*, en los que se sincronizan los números de secuencia y de reconocimiento de los paquetes entre los dispositivos. Este procedimiento es fundamental para una conexión confiable y segura a través de *TCP*.

![[Pasted image 20230410072747.png]]

Y esto lo podemos ver de manera super clara, si nos abrimos el *wireshark* (Herramienta para analizar trafico de red con interfaz grafica) y nos ponemos en escucha el la interfaz "Loopback (lo)" o mismo desde *tshark* en escucha con el parametro -i con esta misma interfaz, e intentamos establecer una conexión con nosotros mismos podriamos ver esto. 

```Shell
# Primero nos ponemos en escucha por el puerto 4646. 
sudo nc -nlvp 4646

# Ahora desde otra consola nos ponemos en con tshark a escuchar el trafico de la interfaz lo, o abrimos el wireshark y lo mismo. 
tshark -i lo 

wireshark &>/dev/null & disown 

# Y por ultimo nos intentamos conectar mediante netcat a nuestra ip por el puerto 4646. 
nc {dirección_ip} 4646 
```

De esta manera veriamos este famoso *Three-Way Handshake*, el cual se tramiten 3 paquetes. 

- #### Desde *wireshark*: 
![[Pasted image 20230410073756.png]]

- #### Desde *tshark*: 
![[Pasted image 20230410073928.png]]

##### Entre otras cosas, tenemos los puertos más basicos: 

TCP:
- ##### 21 -> **FTP** (File Transfer Protocol) Permite la transferencia de archivos entre sistemas.
- ##### 22 -> **SSH** (Secure Shell) Permite a los usuarios conectarse y administrar sistemas de forma remota. 
- ##### 23 -> **Telnet** Permite conexiones remotas a dispositivos de red.
- ##### 25 -> **SMTP** (Simple Mail Transfer Protocol) Permite el intercambio de mensajes de correo electrónico entre dispositivos.
- ##### 53 -> **DNS** (Domain Name Service) Sistema que traduce nombres de dominos a direcciones IP.
- ##### 80 -> **HTTP** (Hypertext Transfer Protocol) Se utiliza para la transferencia de datos en la World Wide Web (www). 
- ##### 110 -> **POP3** (Post Office Protocol) Permite descargar copias de tus mensajes de mail a tu computadora.
- ##### 139, 445 -> **SMB** (Service Message Block) Protocolo que permite transferir archivos entre dos hosts y controla acceso a archivos y directorios
- ##### 143 -> **IMAP** (Internet Message Access Protocol) Permite leer, modificar, eliminar, etc. mails de manera que los cambios se vean reflejados 
- ##### 443 -> **HTTPS** (Hypertex Transfer Protocol Secure) Protocolo que se utiliza para la transferencia de daots encriptaods en la World Wide Web (www). 

UDP: 
- ##### 53 -> **DNS** (Domain Name Service) Sistema que traduce nombres de dominios a direcciones IP.
- ##### 67, 68 -> **DHCP** (Dynamic Host Configuration Protocol) Protocolo utilizado para asignar direcciones IP y otros parámetros de configuración a los dispositivos en una red.
- ##### 69 -> **TFTP** (Trivial File Transfer Protocol) Protocolo que premite transferir archivos entre dispositivos en una red, a diferencia del FPT, este es más simple, no proporciona autenticación de usuarios, ni control de acceso, ni permite caracteristicas de listado de directorios ni cifrado/texto.
- ##### 123 -> **NTP** (Network Time Protocol) Utilizado para sincronizar los relojes de los dispositivos en una red.
- ##### 161 -> **SNMP** (Simple Network Management Protocol) Utilizado para administrar y supervisar dispositivos en una red. 

-----------

# Subneting: 

- ## ¿ Que es?

Consiste en dividir una red en subredes. Hay que tener mucho cuidado para no desaprovechar direcciones IPv4.  Esto se logra mediante el use de *máscaras de red*, que permiten defini qué bits de la dirección IP corresponden a la *red* y cuáles a los hosts.

- ## Interpretar la *Netmask*

Para interpretar una máscara de red, se deben identificar los bits que están en 1. Estos bits representan la porción de la dirección IP que se corresponde a la red. Por ejemplo, una máscara de red de *255.255.255.0* indica que los primeros *tres octetos* de la dirección IP corresponden a la *red*, mientras que el *último octeto* se utiliza para identificar los hosts.

Cuando hablamos de *CIDR* (Classless Inter-Domain Routing), a lo que nos referimos es a un método de asignación de direcciones IP más eficiente y flexible que el uso de clases de reded IP fijas, Con *CIDR*, una dirección IP se representa mediante una dirección IP base y una máscara de red, que se escriben juntas separadas por una "/". 
Por ejemplo, la dirección IP *192.168.1.38* con una máscara de red de *255.255.255.0* se escribiría como *192.168.1.38/24*

La máscara de red se representa en notación de prefijo, que indica el número de bits que están en "*1*" en la máscara. En este caso, la máscara de red *255.255.255.0* tiene 24 bits en "*1*" (Los primeros tres octetos), por lo que su notación de prefijo es /24.

Para calcular la máscara de red a partir de una notación de prefijo, se deben escribir los bits "*1*" en los primeros bits de una direccion IP de 32 bits y los bits "*0*" en los bits restantes. Por ejemplo, la máscara de red */24* se calcularía como *11111111.11111111.11111111.00000000* en binario, lo que equivale a *255.255.255.0* en decimal.

Esto se podria representar en una excel, en donde empezando a partir de los 128 bits, vamos partiendo a la mitad hasta llegar al 1, cuatro veces. 
El resultado de 255 es la operatoria de la suma de la multiplicación que tiene el 128 * el 1 o el 0, dependiendo en que este.

De manera que el primer resultado seria en excel la siguiente operatoria:
#### `=(A1*A2)+(B1*B2)+(C1*C2)+(D1*D2)+(E1*E2)+(F1*F2)+(G1*G2)+(H1*H2)`

![[Pasted image 20230410101337.png]]

Mientras que el valor de /24 sale de la operatoria de contar cuantos valores estan en 1.  En excel, la sig. operatoria:
#### `=CONCATENAR("/";CONTAR.SI(A2:AI2;1))`

En cuanto a clases de direcciones IP, existen tres tipos de máscaras de red: *Clase A*, *Clase B* y *Clase C*.

- ## *Clase A*: 
#### Las redes de *Clase A* usan una máscara de subred predeterminada de *255.0.0.0* y tienen de 0 a 127 como su primer octeto. La dirección *10.52.36.11*, por ejemplo, es una dirección de *Clase A*. Su primer octeto es 10, que está entre 1 y 126, ambos incluidos.

- ## *Clase B:* 
#### Las redes de *Clase B* usan una máscara de subred predeterminada de *255.255.0.0* y tienen de 128 a 191 como su primer octeto. La dirección *172.16.52.63*, por ejemplo, es una dirección de *Clase B*. Su primer octeto es 172, que está entre 128 y 192, ambos incluidos.

- ## *Clase C*: 
#### Las redes de *Clase C* usan una máscara de subred predeterminada de *255.255.255.0* y tienen de 192 a 223 como su primer octeto. La dirección *192.168.123.132*, por ejemplo, es una dirección de *Clase C*. Su primer octeto es 192, que está entre 192 y 223, ambos incluidos.

Es importante tener en cuenta que, además de estos tres tipos de máscaras de red, también existen máscaras de red personalizadas que se pueden utilizar para crear subredes de diferentes tamaños de una red. Recordemos que los *CIDRs* son un método de asignación de direcciones IP que permite dividir una dirección IP en una parte que identifica la *red* y otra parte que identifica el *host*. Esto se logra mediante el uso de una máscara de red, que se representa en notación *CIDR* como una dirección IP base seguida de un número que indica la cantidad de bits que corresponden a la red. 
De esta manera se puede facilitar la administración de red y la desperdiciación de IP's. 

De esta manera, como atacante, basandonos en la máscara de red, o mismo desde una ip,  podriamos empezar a conseguir la netmask, el total de hosts a repartir, el network ID y la broadcast address. 

Esto lo podriamos hacer en base a nuestro anterior excel sumado a uno nuevo: 

![[Pasted image 20230410112448.png]]

En base a esta configuración podriamos ir modificando los distintos valores de bits viendo por un lado como se afectaria la netmask, ya que, en este ejemplo, tenemos las 3 primeras tablas todas con el valor del bit en "*1*" mientras que la ultima todo en "*0*", dejando asi una *netmask de 255.255.255.0* con un total de *256* hosts posibles a signar y un prefijo de */24*, por lo que sabemos que esto seria una netmask de *Clase C* y en base a la ip podriamos averiguar tanto el Network ID como la Broadcast adress, ya que sabemos que la primera IP dentro de las 256 posibles (En este caso) pertenecen al Network ID, y la ultima a la Broadcast Address.

![[MacheteNetmask.png]]

En esta imagen tenemos un pequeño "machete", en donde podemos ver rapidamente las clases de las netmask, junto a el valor x donde se cambiaria por el valor de la columna roja asi como tambien dependiendo el prefix "/x" cuantos hosts disponibles tendriamos. Pero para llegar a esto se lo hace con las sigs. formulas: 

- # Cálculo de la máscara de red:

La dirección IP que se nos da, supongamos *"192.168.1.0/26"*, tiene los primeros 26 bits de la dirección IP que corresponden a la *red* y los últimos 6 bits (Recordemos que maximo son 32, es decir 4 bloques de 8bits) corresponden a los hosts. 
Para calcular la máscara de red, necesitamos colocar los primeros 26 bits en 1 y los útimos 6 en 0: 

- ## 11111111.11111111.11111111.11000000

El valor de los primeros 24 bits (Los primeros 3 bloques) son todos de 1, lo que significa que el valor decimal de cada uno de los octetos es de 255, ya que si tenemos en cuenta que el valor de cada bloque es de 255 devido a lo sig: 

![[Pasted image 20230410113952.png]]

El ultimo octeto tiene los útimos 6 bits en 0, lo que significa que su valor decimal es 192 devido a lo sig: 

![[BITS_De_Un_Byte.png]]

Por lo tanto, la máscara de red es *255.255.255.192*. 

- # Cálculo del total de hosts a repartir: 

En este caso, se pueden utilizar los 6 bits que quedan disponibles para representar la parte de hosts. En una máscara de red de 26 bits, los 6 bits restantes representan: 

- ## 2^6 - 2 = 62

Lo que nos indica que tenemos un total de 62 hosts disponibles para asignar. La formula es de *2^(n) - 2*, donde *n* es la cantidad de bits utilizados para representar la parte de hosts en la máscara de red y el *-2* debido a el Network ID y la Broadcasta Address.

- # Cálculo del Network ID: 

Para calcular el *Network ID*, lo que debemos hacer es aplicar la máscara de red a la dirección IP de la red. En este ejemplo, la máscara de red era *255.255.255.192*, lo que significa que los primeros 26 bits de la dirección IP pertenecen a la parte de red.  
Entonces, para calcular la Network ID, convertiremos tanto la dirección IP como la máscara de red en binario y luego hacemos una operación "*AND*" lógica entre los dos. La operación "*AND*" compara los bits correspondientes en ambas direcciones y devuelve un resultado en el que todos los bits coincidentes son iguales a "*1*" y todos los bits no coincidentes son iguales a *0*.

En este caso, la dirección IP es *192.168.1.0* en decimal y se convierte a binario en 11000000.10101000.00000001.00000000 y la máscara de red que es *255.255.255.192* en decimal se convierte en binario como 11111111.11111111.11111111.11000000. 

Luego, aplicamos la operación "*AND*" entre estos dos valores binarios bit a bit. Los bits correspondientes en ambos valores se comparan de la sig manera: 

![[ANDOperation.png]]

En el caso de que haya dos 1 se convierte a 1, si no, a 0.  Y para convertir el valor de el binario a la dirección ip resultatnte como *Network ID*, podemos hacer lo sig: 

```shell

echo "$(echo "ibase=2; 11000000" | bc).$(echo "ibase=2; 10101000" | bc).$(echo "ibase=2; 00000001" | bc).$(echo "ibase=2; 00000000" | bc

# Esto devolveria 192.168.1.0
```


- # Cálculo de la Broadcast Address: 

La *Broadcast Address* es la dirección de red que se utiliza para enviar paquetes a todos los hosts de la subred. Para calcularla, necesitamos saber el *Network ID* y la *cantidad de hosts* disponibles en la subred. 

En este caso teniamos el *CIDR*  -> /26, estos 26 bits correspondientes a la red y los 6 bits restantes correspondientes a los hosts disponibles, lo que hay que hacer para calcular la Broadcast Addres es converir la *Network ID* a binario "*11000000.10101000.00000001.00000000*" y rellenar los bits disponibles para la signación de hosts con "*1*", dando como resultado: 

## 11000000.10101000.00000001.00111111 = 192.168.1.63 

Una vez más esto lo podemos saber haciendo: 

```shell

echo "ibase=2; 11000000" | bc).$(echo "ibase=2; 10101000" | bc).$(echo "ibase=2; 00000001" | bc).$(echo "ibase=2; 00111111" | bc
```

Con todo esto podemos interpretar de manera rapida los rangos de red que el cliente nos ofrece para auditar.

-----------

# Firewalls

![[Firewall.png]]

Los firewalls son un dispositivo en la red que monitorean el trafico de la misma y son diseñados para proteger las redes y sistemas de posibles amenazas. 

Muchas veces cuando hay un firewall arroja resultados *filtrados* en un escaneo de nmap. 

Algunas tecnicas junto a su parametro de [[Nmap]] a continuación: 

- ## MTU (-mtu): 
La técnica de evasión de *MTU* o "*Maximum Transmission Unit*" implica ajustar el tamaño de los paquetes que se envían para evitar la detección por parte del  Firewall. Nmap permite configurar manualmente el tamaño máximo de los paquetes para garantizar que sean lo suficientemente pequeños para parasar por el Firewall sin ser detectados. (Multiplo de 8 el valor)

- ## Data Length (--data-length):
Esta técnica se base en ajustar la *longitud de los datos* enviados para que sean lo suficientemente cortos como para pasar por el Firewall sin ser detectados. Nmap permite a los usuarios configurar manualmente la longitud de los datos enviados para que sean lo suficientemente pequeños para evadir la detección del Firewall. El length minimo de un paquete que envia nmap, siempre va a ser de 58, pero este valor lo podemos alterar sumandole lo que pongamos como número como arg del --data-length
`sudo nmap -p22 192.168.1.1 --data-length 21`
![[FirewallLenght.png]]

- ## Source Port (--source-port): 
Esta técnica consiste en configurar manualmente el número de *puertos de origen* de los paquetes enviados para evitar la detección por parte del Firewall. Nmap permite a los usuarios especificar manualmente un puerto de origen aleatorio o un puerto específico para evadir la detección de Firewall. Basicamente nmap lo que hace es abrir un puerto aleatorio para poder establecer conexión, pero con este ataque podemos ingresar un puerto en particular.
`nmap {to_scan_ip} --source-port 53`

![[SYNACKRST.png]]


- ## Decoy (-D):
Esta técnica de evasión en Nmap permite al usuario enviar *paquetes falsos* a la red para confundir a los sistemas de detección de intrusos y evitar la detección de Firewall. El comando -D permite al usuario enviar paquetes falsos junto con los paquetes reales de escaneo para ocultar su actividad. Basicamente con el parametro -D podemos ingresar una o unas IP's falsas para enviar estos paquetes falsos, una vez más, con wiresharw o tshark podriamos ver esto: 
`nmap -p22 -D 11.11.11.11 {to_scan_ip}` 

![[FirewallIPS.png]]
Si hicieramos un ataque Decoy con muchas ip, podriamos filtrar con wireshark los apquetes que tengan de destino nuestra IP especificada con `ip.dst == {to_scan_ip}`


- ## Fragmented (-f): 
Esta técnica se basa en *fragmentar los paquetes* enviados para que el Firewall no pueda reconocer el tráfico como un escaneo. La opción -f en Nmap permite fragmentar los paquetes y enviarlos por separado para evitar la detección del Firewall. 
Para ver los paquetes fragmentados desde wireshark podriamos ingresar  `ip.flags.mf == 1`

![[FirewallFramentation.png]]


- ## Spoof-Mac (--spoof-mac): 
Esta técnica de evasión se basa en *cambiar la dirección MAC* del paquete para evitar la detección del Firewall. Nmap permite configurar manualmente la dirección MAC ( Explicada en [[Basic Concepts]]) para evitar la detección. 

- ## Stealth Scan (-sS): 
Esta técnica es una de las más usadas para realizar escaneos sigilosos y evitar la detección del Firewall. El comando -sS permite a los usuarios realizar un escaneo de tip *SYN sin establecer una conexión completa*, lo que permite evitar la detección. Esto lo que hace es lo sig:

![[ThreeWayHandshake.png]]

En una conexión exitosa normal, se tramita un paquete SYN, donde el host responde con un paquete SYN/ACK, en caso de estar cerrado con un RST package, para posteriormente en caso de que este disponible enviar un paquete ACK y establecer la conexión. Al utilizar el Stealth Scan lo que hacemos es enviar el paquete SYN, nos responde con SYN/ACK o RST, depende su estado, y si esta disponible, en lugar de enviar un ACK enviamos un RST para no terminar de completar la conexión, de esta manera sabemos que el host esta disponible pero no nos conectamos, siendo asi más sigilosos.


- ## Min-rate (--min-rate): 
Esta técnica permite al usuario *controlar la velocidad de los paquetes* enviados para evitar la detección del Firewall. El comando --min-rate permite al usuario reducir la velocidad de los paquetes enviados para evitar ser detectado.
 
Obviamente existen más tecnicas para evasión de firewall, pero estas son de las más populares. 
