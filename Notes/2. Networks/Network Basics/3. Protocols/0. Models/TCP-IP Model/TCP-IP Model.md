# TCP/IP Model

El modelo TCP/IP también es un modelo de referencia en capas, a menudo denominado *Internet Protocol Suite*. La diferencia de este con el [[OSI Model]] es que TCP/IP es un modelo más práctico y usado en la vida real, mientras que el modelo OSI es un modelo más didáctico y de referencia.

Similar al Modelo OSI, el modelo TCP/IP se divide en capas, solamente que en este caso contamos con *cuatro* (*4*). Algunas de estas capas (*Application* y *Link*) fucionan más de una capa del modelo OSI.

| Layer | Layer Name                       | Description                                                                                                                                                                                                                                               |
| ----- | -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `4`   | **Application**                  | Gestiona las sesiones y diálogos entre aplicaciones, traduce y convierte los datos, además de que representa datos para el usuario. En otras palabras, combina las funciones de las capas de *Application*, *Presentation* y *Session* del [[OSI Model]]. |
| `3`   | **Transport**                    | Capa responsable de gestionar la entrega de datos, reenvío y control de flujo, admitiendo la comunicación entre distintos dispositivos a través de diversas redes.                                                                                        |
| `2`   | **Internet**                     | Determina el mejor camino a través de una red, encargandose del direccionamiento lógico y del enrutamiento.                                                                                                                                               |
| `1`   | **Network Interface** / **Link** | Controla los dispositivos del hardware y los medios que forman la red, encargandose de colocar los paquetes en el medio de red.                                                                                                                           |

Con TCP/IP, cada aplicación puede transferir e intercambiar datos a través de cualquier red, y no importa dónde esté ubicado el receptor. IP garantiza que el paquete de datos llegue a su destino y TCP controla la transferencia de datos y garantiza la conexión entre el flujo de datos y la aplicación. La principal diferencia entre TCP/IP y OSI es la cantidad de capas, algunas de las cuales se han combinado.

![[OSI_TCP_IP_LAYERS 1.png]]

Las tareas más importantes del modelo *TCP/IP* son:

- **Logical Addressing / Direccionamiento lógico** (*Protocolo IP*): Debido a que hay muchos hosts en diferentes redes, existe la necesidad de eestrucutrar la topología de la red y el direccionamiento lógico. Dentro de TCP/IP, IP asume el direccionamiento lógico de redes y nodos. Los paquetes de datos sólo llegan a la red donde se supone que deben estar. Los métodos para hacerlo son clases de red, subredes y CIDR. 
- **Routing / Enrutamiento** (*Protocolo IP*): Para cada paquete de datos, se determina el siguiente nodo en cada nodo en el camino desade el remitente al receptor. De esta manera, un paquete de datos se enruta a su receptor, incluso si el remitente desconoce su ubicación.
- **Error & Control Flow / Error y flujo de control** (*Protocolo TCP*): El remitente y el receptor frecuentemente están en contacto entre sí a través de una conexión virtual. Por lo tanto, se envían mensajes de control continuamente para comprobar si la conexión aún está establecida.
- **Name Resolution / Resolución de nombres** (*Protocolo DNS*): DNS proporciona resolución de nombres a través de nombres de dominio completos (FQDN) en direcciones IP, lo que nos permite llegar al host deseado con el nombre especificado en Internet.