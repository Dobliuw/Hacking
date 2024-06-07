# [WiFi Pineapple](https://docs.hak5.org/wifi-pineapple)
La **WiFi Pineapple** es una herramienta de auditoría de redes inalámbricas desarrollada por [Hak5](https://hak5.org/). Es bastante conocida en el mundo de la ciberseguridad por la capacidad de realizar diversas prueba de penetración y ataques, así como análisis de redes WiFi. Esta facilita la creación de ataques como MITM, Rogue AP, recopilación de datos, evil twin attack, y otros muchos vistos en [[Hacking WiFi]].

Algunas de sus características principales son...

- *MITM* (*Man-In-The-Middle*): Permite interceptar y manipular el tráfico de los dispositivos conectados.
- *Rogue AP* (*Access Point*): Puede crear un punto de acceso falso para atraer a usuarios a conectarse y luego capturar su tráfico.
- *Sniffing*: Capturar paquetes de datos en la red para su posterior análisis.
- *Deauthentication Attacks*: Expulsa a los clientes de su red para forzarlos a conectarse a la Pineapple.
- *Modularity*: Soporta módulos adicionales que pueden iinstalarse para expandir su funcionalidad.

---
# Power Up 
Para conectar la WiFi Pineapple para posteriormente conectarnos, podemos hacer uso de esta [guía](https://docs.hak5.org/wifi-pineapple/setup/connecting-the-wifi-pineapple) proporcionada por Hak5. 

---
# [Setup](https://docs.hak5.org/wifi-pineapple/setup/setting-up-your-wifi-pineapple)
Una vez iniciada la Pineapple, deberemos hacer una configuración de la misma, la cual conlleva la instalación del último Firmware, así como la configuración de conexión a internet, usuario, contraseña, etc.

Primero que nada, con el comando `ifconfig` o `ipconfig` (Depende nuestro sistema operativo) podremós ver las interfaces de red que tenemos, en caso de haber utilizado al usb para conectar la Pineapple a la PC, veriamos que tenemos una intefaz de red con el segmento de red **172.16.42.0/24** donde la IP *172.16.42.1* será nuestro WiFi Pineapple, y podremos acceder mediante el navegador al puerto *1471* para llevar a cabo la gestion web mediante GUI.

Nos pedirá que nos conectemos a nuestra red local para poder disponer de conexión a internet y descargar e instalar la última versión del Firmware:

![[download_latest_firmware_pineapple_hak5.png]]

Tras la descarga e instalación del Firmware, se nos solicitaran algunas configuraciones, incluyendo la contraseña para el usuario por el cual podrémos acceder al portal web de configuración o conectarnos a través de ssh a la pineapple. Tras la finalización de estas configuraciones, se nos redireccionará automaticamente a la web final, la cual dispondrá de un login con las credenciales previamente configuradas.

- Acceder mediante *ssh*: 
```bash
ssh root@172.16.42.1
```

----
# Network Interfaces
La WiFi Pineapple Mark VII utiliza múltiples interfaces de red para diferentes propósitos, permitiendo realizar diversas tareas de auditoría y pruebas de seguridad. A continuación vamos a describir algunas de estas y su uso típico.
###### br-lan (Bridge LAN)
Esta interfaz es un puente de red que combina múltiples interfaces en una sola, proporcionando una única dirección IP para acceder a la Pineapple, en la mayoría de casos, configurada con la IP *172.16.42.1*. El uso típico de esta es para la gestion de red interna y acceso a la GUI o SSH.

###### eth0 (Ethernet)
Esta interfaz es la conexión a través del puerto USB-C de la Pineapple. Se utilizap ara conectar la misma a una red cableada o directamente a un equipo, lo que permite el acceso a internet o transferencia de datos.

###### lo (Loopback)
Esta interfaz virtual es utilizada para la comunicación interna del sistema para diagnósticos de red y comunicación interna.

###### wlan0 (Open)
Interfaz inalámbrica principal que puede ser utilizada para diversos propósitos como escaneo de redes o actuación como cliente. Se suele utilizar para escaneo de redes WiFi y conexión a redes abiertas.

- Configuración de ejemplo
```bash
# Validate attributes and details like ssid, channel, etc
iw dev wlan0 info
# Validate additional info
iw dev wlan0 link
```

###### wlan0-1 (Management)
Subinterfaz de *wlan0* dedicada a la gestión de la Pineapple, generalmente utilizada para la conexión GUI de la misma, así como para la gestión y configuración a través de la interfazweb.

###### wlan0-2 (Evil Enterprise)
Subinterfaz de *wlan0* configurara para ejecutar ataques de **Evil Enterprise**, que imitan redes corporativas para capturar credenciales creando puntos de accesos falsos.

- Configuración de ejemplo
```bash
ifconfig wlan0-2 up
hostapd /etc/hostapd/evil-enterprise.conf
```

###### wlan0-3 (Evil WPA)
Subinterfaz de *wlan0* configurada para ejecutar ataques de **Evil WPA**, craendo puntos de acceso falsos para capturar claves *WPA/WPA2*.

- Configuración de ejemplo
```bash
ifconfig wlan0-3 up
hostapd /etc/hostapd/evil-wpa.conf
```

###### wlan1mon (Recon)
Interfaz configurada en modo monitor, utilizada para tareas de reconocimiento y escaneo de redes, permite capturar apquetes y analizar el tráfico de red.

- Configuración de ejemplp
```bash
ifocnfig wlan1mon up
# Start wlan1mon interface
airmon-ng start wlan1mon
# Kill some process 
airmon-ng check kill
# Sniff trafic
airodump-ng wlan1mon
```

###### wlan2 (Wireless Client)
Interfaz que actúia como cliente inalámbrico, permitiendo que la Pineapple se conecte a otras redes WiFi de manera inalambrica.

----
# SSID Filter & Client Filter (Allow/Deny list)

La WiFi Pineapple Mark VII incluye funcionalidades avanzadas de filtrado para gestionar cómo interactúa con redes y clientes. Estas funcioanlidades son cruciales para realizar pruebas de epentración específicas y controladas.
###### SSID Filter
El *SSID Filter* se usa para gestionar qué redes inalámbricas (SSIDs) serán atacadas o con las cuales interactuaremos. En caso de hacer uso de **Allow List**, los SSIDs que están en este lista serán atacados, mientras que si hacemos uso de **Deny List**, los SSIDs en está serán ignorados.

Para a gregar SSIDs podemos hacer uso de la GUI o del comando `pineap` para llevar a cabo esto:

```bash
# Add ssid to the list
pineap add_filter_ssid {ssid}
# Delete ssid from the list
pineap del_filter_ssid {ssid}
```

###### Client Filter
El *Client Filter* se usa para gestionar qué dispositivos (clientes) serán atacados o con los cuales se interactuará. Similar al SSID Filter, podemos configurar los filtros de clientes de la misma manera, haciendo uso de **Allow List** para indicar que clientes serán atacados y **Deny List** para indicar aquellos que serán ignorados.

También podemos agregar los clientes haciendo uso de la GUI de la página web o con el comando `pineap`:

```bash
# Add client to the list
pineap add_filter_mac {mac}
# Delete client from the list
pineap del_filter_mac {mac}
```

![[client_and_ssid_lists_filters_pineapple.png]]