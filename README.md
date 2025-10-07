# Dobliuw Hacking notes 

<html>
<center>
<img src="./0. Images/w_og.jpeg" width=50%/>
</center>
</html>

Bienvenido/a. Esta sección de mi web reúne mis notas técnicas desarrolladas a lo argo de mi desarrollo personal y experiencia en tópicos de **tecnología** y **ciberseguridad**. Aquí encontrarás documentación de conceptos, procedimientos de laboratorios, guías educativas en apartados tecnologícos como redes, sistemas operativos, lenguajes de programación, apuntes y PoC de vulnerabilidades Web y en sistemas, entre muchas cosas más.

----
# Main Content (Notes)

Dentro de las diferentes secciones que encontrarás en esta *personal wiki* o *guía de estudio*, se destacan las siguientes subsecciones (Todas estas secciones serán encontradas dentro de la sección "**Notes**", donde se da comienzo a todos los artículos realizados):

### 🌐 Networks

Esta sección está pensada como punto de partida para cualquiera que quiera entender el mundo digital desde la base. La misma contiene:

- Fundamentos y estructura (Modelo OSI/TPC-IP, PDUs, encapsulación).
- Conceptos y prácticas de configuración (Switching, routing, VLANs, STP, BGP básico).
- Cheatsheets y comandos (Cisco IOS, Linux Networking).
- Laboratorios prácticos con topologías reproducibles y ejemplos de captura de tráfico (Wireshark).
- Subsección para **Redes de Radio Frecuencia** (En progreso): fundamentos de electromagenitsmo, SDR, Blueetooth, NFC, RFID y su seguridad.
### 💽 Sytem

Sección dedicada a sistemas operativos y su ingeniería:

- Arquitectura de OS (Windows y Linux): procesos, gestión de memoria, llamadas al sistema, módulos/servicios.
- Firmware, bootloaders, BIOS vs UEFI, tables de particionado y sistemas de archivos  (FAT32, NTFS, EXT4).
- Herramientas administrativas (Logs, journalctl, Event Viewer).
- Apuntes prácticos sobre compilación, debugging y análisis a bajo nivel (Conceptos de CPU, Assembly Basics, linking, ELF/PE, syscalls).
### 🔒 Cybersecurity

Sección con contenidos transversales sobre seguridad ofensiva y defensiva:

- ###### 🔵 Blue Team (defensiva):
	- OWASP Top 10, mejores prácitas y securización en APIs
	- Monitorización, análisis de logs y correlación de eventos.
	- Tecnologías de ciberseguridad de monitorización de endpoints y sistemas (EDR, SIEM). 
	- Ingeniería inversa y análisis básico de malware.
	- Hardening de sistemas y respuesta ante incidentes.
	- Herramientas de análisis de phishing y mitigación de ataques.

- ###### 🔴 Red Team (ofensiva):
	- Pruebas de penetración y explotación (Vulnerabilidades, PoC, Mitigaciones, Escaladas de privilegios).
	- Configuraciones para entornos de Hacking.
	- Auditoria y ataques a dispositivos móviles (Análisis Statico vs Dinámico), configuración de entornos, procesos.
	- Ataques y conceptos de Hacking de Redes (Pivoting, Spoofing). 
	- Hacking y ataques contra sistemas y webs (Vulnerabilidades, PoC, Herramientas, Frameworks, BOF).
	- Desarrollo de payloads
### 🔧 Technologies

Recopilación y referencias sobre teconologías y lenguajes con enfoque de aprendizaje profundo y/o cheatsheets :

- Lenguajes y scripts (Python, C, PowerShel, Bash con enfoques de explotación).
- Plataformas como Docker y servicios cloud básicos.
- Servicios y su funcionamiento (Kerberos).
- Tecnologías como SQL, MongoDB.
### ⚙️ Hardware

Apuntes y proyectos prácticos de hardware y dispositivos de hacking :

- Electronica y Micrcontroladores (ESP32, Arduino), SBCs (Raspberry Pi).
- Diseño de dispositivos de bosillo para aprendizaje (Dispositivo móvil de hacking con Kali NetHunter + SDR, Bluetooth hacking support).
- Review y uso básico de dispositivos de hacking provenientes de [hak5.org](https://www.hak5.org) (WiFi Pineaple, Mark VII, Rubber Ducky).
- Conceptos básicos de Impresoras 3D.

-----
# Usage and Proyect Contributions

Si queres utilizar en tu entorno local y/o contribuir al proyecto podes:

1. Hacer **fork** en github y crear una rama por feature (O **clonar** únicamente).
2. Descargar [Obsidian](https://obsidian.md/download) para tu sistema operativo.
3. Seleccioná *Arbrir vault* y vinculalo con la carpeta "*Hacking*" clonada.
4. (*Opcional*) Para una mejor experiencia activa la opción *Confiar en el actor....* para descargar los temas y plugins utilizados a la hora de redactar apuntes. 

# Ethical Disclaimer

> [!warning] ADVERTENCIA LEGAL Y ÉTICA
> Los PoC, el conocimiento brindado y las pruebas adjuntas a lo largo de estas secciones son sólo con fines éticos y en pos de volver el mundo digital un lugar más seguro, invito a poner en práctica los conceptos descritos únicamente en entornos personales de laboratorio, plataformas de práctica como *Hack The Box*, *Try Hack Me* o *Vuln Hub* y volverse profesionales del área que consideren que les pertenezca.
> 
> Recuerden que por mucho que logren saber y "cubrir sus huellas", tarde o temprano la vulnerabilidad más grande que disponemos es explotada por nosotros mismos, el ser humanos.
> 
> Happy Hacking, **W**. 
> 

