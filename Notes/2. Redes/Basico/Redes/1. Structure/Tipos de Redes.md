----
- Tags: #redes #basico #teoria 
----
# Network Types / Tipos de redes

Cada red es estructurada de manera diferente y puede ser configurada individualmente. Por esta razón, existen los llamados **types** (Tipos) y **topologies** (Topologias) que pueden usarse para categorizar estas redes.

 ![[common_network_types.png]]
 ![[book_network_types.png]]
###### WAN (Wide Area Network)

La red **WAN** (**Wide Area Network**) mayormente es referida como **Internet**. Cuando estemos manejando equipamiento de redes, mayormente tendremos una dirección *WAN* y una dirección *LAN*. La dirección WAN es la dirección con la que generalmente accedemos a internet, dicho esto, no incluye internet; una WAN es solo una gran cantidad de redes LAN unidas. Muchas empresas grandes o agencias gubernamentales tendrán una "*WAN Interna*" (También llamada intranet, Red Airgap, etc.).
Generalmente, una de las primeras maneras de identificar que estamos en una red WAN es si se utilizan protocolos de enrutamiento específicos como *BGP* y si el IP Schema en uso no está dentro del *RFC 1918* (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16). 

###### LAN (Local Area Network) / WLAN (Wireless Local Area Network)

Las redes **LANs** (**Local Area Networks**) y las **WLANs** (**Wireless Local Area Networks**) normalmente asignarán direcciones IP designadas para uso local (*RFC 1918*, 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16). En alugnos casos, como universidades u hoteles, es posible que se asigne una dirección ip *routable* (Internet) para unirse a la LAN, pero eso es muy poco común. No existe nada diferente entre LAN o WLAN, aparte de que las WLAN introducen la habilidad de trasnmitir datos con la falta de cables.

###### VPN (Virtual Private Network)

Existen tres tipos de **VPNs** (**Virtual Private Networks**), pero las tres tienen el mismo uso de permitir a un usuario sentir que esta conectado a una red diferente.

- *Site-To-Site VPN*: Tanto el cliente como el servidor son dispositivos de la red, habitualmente*routers* o *firewalls*, y comparten el rango de red completo. Esto es muy comúnmente usado para unir redes empresariales a través de internet, lo que permite que varias ubicaciones se comuniquen a través de Internet como si fueran locales.

- *Remote Access VPN*: Esto implica que la computadora del cliente crea una interfaz virtual que se comporta como si estuviera en la red de un cliente. Por ejemplo, páginas como *Hack The Box* hacen uso de **OpenVPN**, que crea un *adaptador TUN* que permite acceder a los recursos necesarios. Al analizar estas VPN, una pieza importante a considerar es la tabla de enrutamiento que se suele crear al unirse a la VPN. SI la VPN solo crea rutas para redes específicas, esto se denomina VPN de túnel dividido, lo que significa que la conexión a Internet no sale de la VPN.

- *SSL VPN*: Básicamente, esta VPN se realiza dentro de nuestro navegador y se está volviendo cada vez más común a medida que nlos navegadores web se vuelven capaces de hacer cosas. Normalmente, estas VPNs transmitiran aplicaciones o sesiones de escritorios enteros a nuestro navegador.
 
###### GAN (Global Area Network)

Una red mundial como *Internet* es conocida como **Global Area Network** (**GAN**). Sin embargo, internet no es la única red informática de este tipo. Las compañias con actividad internacional también mantienen redes aisladas que abarcan varias *WAN* y conectan equipos de la empresa en todo el mundo. Las GAN utilizan la infraestrucutra de fibra de vidrio de redes de área amplia y las interconectan mediante cables submarinos internacionales o transmisión por satélite.

###### MAN (Metropolitan Area Network)

Las redes **MAN** (**Metropoloitan Area Network**) es una red de telecomunicaciones de banda ancha que conecta varias LAN en proximidad geográfica. Por regla general, se trata de sucursales individuales de una empresa conectadas a un MAN mediante líneas arrendadas. Se utilizan enrutadores de alto rendmiento y conexiones de alto rendimineto basadas en fibra de vidrio, que permiten un redimineto de datos significativamente mayor que Internet. La velocidad de transmisión entre dos nodos remotos es comparables a la comunicación dentro de una LAN.

###### PAN (Personal Area Network) / WPAN (Wireless Personal Area Network)

Los dispositivos finales modernos, como smartphones, tablets, laptops o pcs pueden ser conectados para formar una red que permita el intercambio de datos. Esto se puede hcaer por cable en forma de PAN. Mientras que la variante inalámbrica (WPAN) se basa en tecnologías Bluetooh o USB inalámbrico. Una WPAN que se establece mediante Bluetooh se llama *Piconet*. Las PAN y WPAN suele tener sólo unos pocos metros de extensión y, por lo tanto, no son adecuadas para conectar dispositivos en habitaciones separadas o incluso en edificios.
En el contexto del **IoT** (**Internet Of Things**), las WPAN se utilizan para comunicar, controlar y monitorear aplicaciones con bajas velocidades de datos. Protocolos como Insteon, Z-Wave y ZigBee se diseñaron explícitamente para hogares inteligrantes.
