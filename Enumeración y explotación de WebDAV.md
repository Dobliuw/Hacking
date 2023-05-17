----
- Tags: #ataques #basico #teoria #practica 
----

# ¿ Que es **WebDAV** ? 

### **WebDAV (Web Distributed Authoring and Versioning)** es una extensión del protocolo HTTP que permite a los usuarios **acceder** y **manipular** arachivos en un servidor web a través de una conexción segura.

### Cuando hablamos de enumerar un servidor WebDAV, a lo que nos referimos es al proceso de recopilar información sobre los recursos dispobilbles en el servidor WebDAV. Los atacantes pueden utilizar herramientas de enumeración de webDAV para buscar recursos protegidos en el servidor, como archviso de configuración, contraseñas y otros datos confidenciales. Los atacantes pueden utilizar la información recopilada surante la enumeración para planificar ataques más sofisticados contra el servidor. 

----

# Reconocimiento 

### En la fase inicial de reconocimiento, se implica el intentar identificar las **extensiones de archivo** permitidas en el servidor. Una vez detectadas las extensiones de archivo permitiddas, los atacantes pueden aprovecharse de esto para cargar y ejecutar archivos que contengan código malicioso. Si los archivos maliciosos se cargan y ejecutan con éxito en el servidor web, los atacantes pueden obtener acceso no autorizado al sercidor y comprometer la seguridad del sistema. 

### Una de las [[⚒ Herramientas ⚒]] a usar es **Davtest**, la cual es una herramienta de línea de comandos que se utiliza para realizar pruebas de penetración en servidores WebDAV. Esta puede utilizarse para enumerar recursos protegidos en un servidor WebDAV, así com para probar la configuración de seguridad del servidor. Por ultimo, también puede utilizarse para probar la autenticación y la autorización del servidor, y para detectar vulnerabilidades conocidas. 

### Otra de las [[⚒ Herramientas ⚒]] a usar es **Cadaver**, la cual es una herramineta de línea de comandos que se utiliza para interactuar con servidores WebDAV. Permite a los usuarios navegar por los recursos del servidor, cargar y descargar archivos, y ejecutar comandos en el servidor. También puede utilizarse para realizar pruebas de penetración en servidores WebDAV, como la enumeración de recursos protegidos y la explotación de vulnerabilidades conocidas. 

---

# Evitar estos ataques 

### Para  prevenir la **enumeración** y **explotación** de WebDAV, es importante que los administradores de sistemas implementen medidas de seguridad adecuadas en el servidor. Esto puede incluir la limitación de los recursos disponibles en el servidor y la utilización de autenticación y autorización fuertes. Además, es importante que los usuarios protejan sus contraseñas y eviten el uso de contraseñas débiles o fáciles de adivinar. 

----

# Explotación 