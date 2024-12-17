# Welcome and Disclaimer

Bienvenido(a), mi apodo es `Dobliuw` en este maravilloso mundo y este es el comienzo de una serie de *Writeups* que abarcarán máquinas de diversas plataformas y niveles a medida que continue avanzando mi aprendizaje y experiencia. Sin embargo, simpre tuve la necesidad de entender el **WHY?** de cada paso, el trasfondo técnico de cada acción, de cada herramienta seleccionada a utilizar y *cómo se conecta con situaciones reales* en el mundo del hacking ofensivo y defensivo de carácter profesional.

Mis writeups están diseñados par quienes, como yo, buscan ese valor agregado. explicaciones detalladas que conectan las técnicas con el mundo preofsiona y experiencias reales. Por eso, independientemente de lo "CTF" que pueda llegar a ser una máquina, intentaré abordarla desde un enfoque práctico y realista, compartiendo mis pensamientos, posibles escenarios y aprendizajes en el camino.

Aprender a Hackear va más allá de ralizar una máquina, de utilizar un framework automatizado como `Metasploit` o herramientas automatizadas de las cual abundan. El verdadero valor radica en entender la vulnerabilidad explotada, entender el desarrollo de la herramienta automatizada utilizada, el razonamiento detrás del hallazgo de dicha vulnerabilidad, el razonamiento del porque investigar determinado serivicio, el uso de determinada técnica, etc.

Adicionalmente cabe aclarar que este documento mantendrá un *spanglish* el cual es con el fin de retener la terminología utilizada en el primer mundo, donde muchos apuntamos desarrollarnos como profesionales, por lo que considero que estar en constante relación de estos términos y nombres nos permitirá tener una gran parte del trabajo realizada.

Por último, todo lo mencionado y explicado en este artículo y en otros futuros tiene fines educativos y éticos, llevado a cabo en entornos controlados. No me hago responsable del mal uso que terceros puedan darle a esta información.

-----
# LinkVortex HTB Machine

Máquina [LinkVortex](https://app.hackthebox.com/machines/LinkVortex) de **HackTheBox**. 

-----
# Network Enumeration

Como en cualquier proceso de auditoría, comenzamos con la **fase de reconocimiento**. Esta etapa es *crucial* para identificar servicios corriendo en la(s) máquina(s) víctima, versiones de software, configuraciones de infraestructura y otros elementos clave para planificar la **fase de ataque**. 

Es importante tener en cuenta que, en plataformas como [HackTheBox](https://app.hackthebox.com/), la *target IP*/*IP Objetivo* nos es provista por la plataforma web tras hacer uso de una conexión *VPN*. Sin embargo, si bien esta información también podría ser dada por un cliente marcando el *Scope*/*Alcance* de la auditoría, en otros casos, necesitaríamos descubrir los posibles dispositivos víctima u objetivos mediante técnicas de reconocimiento y enumeración de red.

Una de estas técnicas es la **enumeración de red local**, que puede realizarse usando protocolos como el **Address Resolution Protocol** (**ARP**) que mapea direcciones de Capa 2 **Media Access Control** (**MAC**) con direcciones de Capa 3 **Internet Protocol** (**IPv4**/**IPv6**) del Modelo OSI y Modelo TCP/IP. Aunque también podríamos usar servicios como **Internet Mesage Control Portocol** (**ICMP**) para hacer ping a los dispositivios, posibles restricciones de firewall podrían bloquear nuestras solicitudes.

Para entender más en profundidad el funcionamiento de Capa 2 y Capa 3, junto a sus respectivos protocolos, recomiendo hacer uso de los apuntes que desarrolle basadome en toda la cursada del CCNA 1 impartida por Cisco Academy:

- [[0. Data Link Layer]].
	- [[1. Sublayer MAC]].
- [[0. Network Layer]]
	- [[2. IPv4 Addresses - Direcciones IPv4]].
	- [[3. IPv6 Address Type]]

#### Linux/Unix arp enumeration

`arp-scan` es una herramienta poderosa para explorar redes locales mediante ARP. A contiuación, un ejemplo práctico para ejecutarla: 

```bash
sudo arp-scan -I {interface} --localnet --ignoredups
```
- `-I`: Especificar la interfaz de red a usar (Por ejemplo *eth0*, *ens33*, etc.)
- `--localnet`: Escanea todo el rango de IPs de la red local.
- `--ignoredups`: Ignora respuestas duplicadas obtenidas.

#### Windows arp enumeration

En Windows también podriamos hacer uso de herramientas como [arp-scan windows](https://github.com/QbsuranAlang/arp-scan-windows-) donde podremos hacer un escan de una red.

Este ejecutable *.exe* podríamos alojarlo en la ruta `C:\Windows\System32` para hacer alusión al mismo sin la necesidad de ingresar la ruta absoluta, o bien modificar la variable de entorno `PATH` con la ruta deseada en la cual queramos tener nuestro ejetuable.

- Uso `arp-scan` descargado:
```cmd
arp-scan -t {NetworkIP}/{CIDR}
``` 

#### Windows and Linux ARP Table Listing

En caso de no disponer de herarmientas adicionales, tanto Linux como Windows permiten *listar la tabla ARP* ([[1. ARP - Address Resolution Protocol]]) de la red actual con comandos nativos, ambos sistemas operativos comparte esté comando:

```cmd
arp -a 
```

---
# Enumeration

Una vez obtenida la(s) dirección(es) IP objetivo, comienza la fase de reconocimiento, en este punto deberemos tratar de identifiar puertos, servicios, infraestructura de la máquina víctima. Para esto podemos hacer uso de herramientas como `nmap` para llevar a cabo la enumeración incial.

 - Detección de puertos abiertos de la *target IP*:
```bash
sudo nmap -p- --open --min-rate 5000 -n -vvv -sS 10.10.11.47 -oG allPorts
```
- `-p-`: Escaneo a los 65.535 puertos.
- `--open`: Únicamente puertos abiertos.
- `--min-rate 5000`: Paquetes no más lento que 5000 por segundo.
- `-n`: No realizar resolución DNS.
- `-vvv`: Verbose al máximo nivel.
- `-sS`: Realizar la técnica *Stealth Scan* ([[Basic Concepts#Stealth Scan (-sS)]]) en la evasión de posibles firewalls, consiste en no completar la conexión TCP con el tipico paquete `ACK` hacia el servidor, si no, reemplazarlo por un paquete con la flag `RST` para finalizar la conexión con el servidor en el proceso *Three Way Handshake* ([[1. TCP Process Comunication#Three Way Handshake]]).
- `-oG`: Exportar hallazgo en formato grepeable.

Una vez realizado el escaneo logramos detectar que en este caso la IP tiene expuestos el puerto `22` y  `80` , lo que nos da a pensar en un posible **Secure Shell** (**SSH** - *Puerto 22*) y **Hyper Text Transfer Protocol** (**HTTP** - *Puerto 80*). 

En mi caso dispongo de una utilidad copartida por el grande de S4vitar la cual se encuentra en la `~/.zshrc` o `~/.bashrc` llamada *extractPorts* que nos permite extraer los puertos encontrados en el escaneo de un archivo con el stdout de nmap en el formato específicado con la flag `-oG` de nmap:

- *extractPorts*:
```bash
extractPorts () {
	ports="$(cat $1 | grep -oP '\d{1,5}/open' | awk '{print $1}' FS='/' | xargs | tr ' ' ',')" 
	ip_address="$(cat $1 | grep -oP '\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}' | sort -u | head -n 1)" 
	echo -e "\n[*] Extracting information...\n" > extractPorts.tmp
	echo -e "\t[*] IP Address: $ip_address" >> extractPorts.tmp
	echo -e "\t[*] Open ports: $ports\n" >> extractPorts.tmp
	echo $ports | tr -d '\n' | xclip -sel clip
	echo -e "[*] Ports copied to clipboard\n" >> extractPorts.tmp
	bat extractPorts.tmp
	rm extractPorts.tmp
}
```

Como vemos, la herramienta intenta utilizar plugins como `bat` y herramientas como `xclip` por lo que es necesario tener en cuenta esto para modificarla si es que queremos utilizarla. Ya que si bien en este caso tratandose de únicamente 2 puertos no es necesario, en otros escenarios de máquinas más avanzadas con más servicios expuestos o mismo escenarios reales en máquinas Windows con las que si tengamos conectividad, veremos que serán muchos y esta herramienta nos copiaría todos.

```bash
sudo apt update
sudo apt install xclip
```

- Extraer puertos expuestos reportados por nmap alojados en el archivo *allPorts*:

```bash
extractPorts allPorts
```

Una vez copiado los puertos, proseguiremos con intentar detectar *Version* y *Servicios* que corren para cada uno de estos puertos:

```bash
nmap -p22,80 -sCV 10.10.11.47 -oN portsInfo.py
```
- `-sCV`: Intentar reconocer version y servicio
- `-oN`: Exporter output en formato normal.
- 
En mi caso tiendo a exportar el output a un archivo con terminación *.py* ya que utilizo [batcat](https://github.com/sharkdp/bat) y este reconoce el output como formato Python y le da más vida a la lectura:

![[Pasted image 20241216152806.png]]

Como vemos en el output, Nmap nos indica que no puede realizar la redirección del servidor al dominio `linkvortex.htb`, lo cual nos da indicios de que se puede estar realizando virtual hosting y como sabemos no es lo mismo conectarnos a un recurso mediante su nombre de dominio que con la IP original. En este caso parece ser que el servidor web intentar obtener el recurso de este dominio. Por lo que modificaré mi archivo `/etc/hosts` para que mi dispositivo pueda resolver esta dominio a la IP target.

- Agregar resolución DNS para la IP target:
```bash
sudo echo -e "\n10.10.11.47 linkvortex.htb" >> /etc/hosts
```

Por lo que el contenido del archivo `/etc/hosts` quedaría algo tal que así:

![[Pasted image 20241216153235.png]]

Una vez realizado esto, por casos que me he encontrado en otros CTF elijo vovler a correr el escaneo de Servicios y Puertos de Nmap:

```bash
nmap -p22,80 -sCV 10.10.11.47 -oN portsInfo.py
```

Ahora si como vemos en el output, al `Nmap` correr scripts propios como el `http-enum` detecta archivos como el *robots.txt* el cual nos indica *entradas no permitidas*/*disallowed entries*.

![[Pasted image 20241216152409.png]]

Alcanzado este punto, prosigo con la enumeración web del puerto *80* ya que veo que el puerto *22* (*SSH*) no es inferior a la versión *7*, por lo que de momento, por no tener ninguna credencial no veo una via potencial de abuso del mismo.

Para la enumeración del puerto 80 utilizaré técnicas de **Fuzzing** de *directorios*, *subdominios*, etc. que se mencionan en el artículo [[HTTP-HTTPS Enum]]. El Fuzzing de directorios y archivos con distintas extensiones típicas al sitio web `linkvortex.htb` no llevó a nada, al igual que navegar un rato por la web en búsqueda de funcionalidades, hacer lectura de la consola, procesos de red y cookies almacenadas a través de la consola para desarrolladores, ni la lectura del código fuente en búsqueda de posible información hardcodeada (`Ctrl + U`) por lo que proseguí con el Fuzzing a Subdominios.

Algo adicional que me gustaría agregar, es que en estos casos lo que suelo hacer es configurar el  *Proxy* de `Burpsuite` ([[Burpsuite]]) para que todo el "scraping" manual que realizo en la web se vaya almacenando en la pestaña de *Proxy* > *HTTP history*.

- Enumeración de *subdominios*: 
```bash
gobuster vhost -u http://linkvortex.htb -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-20000.txt -t 100 --append-domain -o linkvortex.htb_subdomains.txt
```

En mi caso partícular me gusta utilizar la herramienta `tee` o flags personalizadas de las herramientas (Como es el caso `-o`) para guardar el output de todos los escaneos que voy realizando, de esta menra me permite ahorrar tiempo en un futuro en caso de tener que reveer los outputs obtenidos en determinada parte del proceso a la vez que ir guardando la evidencia en una estructura de directorios personal donde recurriré en la etapa final de redacción de informe.

Recordemos que todo es cuestion de **Metodología**, acostumbrarnos a adoptar esta u otras metodologías que nos queden comodas nos hará ser mejor en nuestra trabajo.

Como vemos el output de nuestra escaneo es el siguiente:

![[Pasted image 20241216154526.png]]

Esto indica que existe un subdominio nuevo (`dev.linkcvortext.htb`) el cual podremos analizar, ampliando así nuestra superficie de ataque. Este dominio deberá ser agregado al `/etc/hosts`.

Una vez agregado, llevaré a cabo nuevamente una enumeración de posibles archivos y extensiones.

```bash
gobuster dir -u http://dev.linkvortex.htb -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 100 -o dev.linkvortex.htb_dirs.txt
```

En este caso, al cabo de un rato vemos que no encontramos nada de interes. En este caso me gusta utilizar otro diccionario adicional el cual se encuentra en el proyecto de [SecLists](https://github.com/danielmiessler/SecLists) y es `/Fuzzing/fuzz-Bo0oM.txt` que nos puede permitir buscar otros posibles archivos ocultos que `/Disocvery/Web-Content/directory-list-2.3-medium.txt` no dispone.

```bash
gobuster dir -u http://dev.linkvortex.htb -w /usr/share/wordlists/seclists/Fuzzing/fuzz-Bo0oM.txt -t 100 | tee -a dev.linkvortex.htb_dirs.txt
```

*Aclaración*: Importante tener en cuenta que cuando realizamos múltiple escaneos con múltiples directorios distintos a un mismo dominio y queremos guardar esta data sin que se sobreescriba, en caso de hacer uso de la utilidad `tee` deberemos hacerlo con su flag `-a` de *append*.

En este caso, al ejecutar el comando, vemos que se encuentra un endpoint `/.git` el cual nos da indicio de un posible repositorio git expuesto. Esto me lleva a pensar automáticamente en técnicas para recuperar este repositorio y así poder dar una mayor vista en profundidad a la posible arquitectura de la web, o en caso de ser un proyecto de alguna otra cosa, buscar credenciales hardcodeadas, cambios realizados en commits, etc.

