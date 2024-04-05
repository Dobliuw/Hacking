----
- Tags: #redes #basico #teoria 
----
# TCP/IP MOdel

El modelo TCP/IP también es un modelo de referencia en capas, a menudo denominado *Internet Protocol Suite*. El término TPC/IP hace referencia a los dos protocolos: *Transmission Control Protocol* (*TCP*) y *Internet Protocol* (*IP*). IP se encuentra dentro de la capa de red (Capa 3) y TCP se encuentra dentro de la capa de transporte (Capa 4) del [[Modelo OSI - OSI Model]].

- ##### **4) Aplication:** La capa de aplicación permite que las aplicaciones accedan a los servicios de otras capas y define los protoclos que utilizan las aplicaciones para intercambiar datos.
- ##### **3) Transport:** La capa de transporte es responsable de proporcionar servicios de sesión (TCP) y datagramas (UDP) para la capa de aplicación.
- ##### **2) Internet:** La capa de internet es responsable de las funciones de direccinamiento, empaquetado y enrutamiento del host.
- ##### **1) Link:** La capa de enlace es responsable de colocar los paquetes TCP/IP en el medio de red y recibir los paquetes correspondientes del medio de red. TCP/IP está diseñado para funcionar independientemente del método de acceso a la red, el formato de trama y el medio.

Con TCP/IP, cada aplicación puede transferir e intercambiar datos a través de cualquier red, y no importa dónde esté ubicado el receptor. IP garantiza que el paquete de datos llegue a su destino y TCP controla la transferencia de datos y garantiza la conexión entre el flujo de datos y la aplicación. La principal diferencia entre TCP/IP y OSI es la cantidad de capas, algunas de las cuales se han combinado.

![[OSI_TCP_IP_LAYERS.png]]

Las tareas más importantes del modelo *TCP/IP* son:

- **Logical Addressing / Direccionamiento lógico** (*Protocolo IP*): Debido a que hay muchos hosts en diferentes redes, existe la necesidad de eestrucutrar la topología de la red y el direccionamiento lógico. Dentro de TCP/IP, IP asume el direccionamiento lógico de redes y nodos. Los paquetes de datos sólo llegan a la red donde se supone que deben estar. Los métodos para hacerlo son clases de red, subredes y CIDR. 
- **Routing / Enrutamiento** (*Protocolo IP*): Para cada paquete de datos, se determina el siguiente nodo en cada nodo en el camino desade el remitente al receptor. De esta manera, un paquete de datos se enruta a su receptor, incluso si el remitente desconoce su ubicación.
- **Error & Control Flow / Error y flujo de control** (*Protocolo TCP*): El remitente y el receptor frecuentemente están en contacto entre sí a través de una conexión virtual. Por lo tanto, se envían mensajes de control continuamente para comprobar si la conexión aún está establecida.
- **Name Resolution / Resolución de nombres** (*Protocolo DNS*): DNS proporciona resolución de nombres a través de nombres de dominio completos (FQDN) en direcciones IP, lo que nos permite llegar al host deseado con el nombre especificado en Internet.