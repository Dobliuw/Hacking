----
- Tags: #redes #basico #teoria 
----
# Network Layer

La *Capa de Red* / *Network Layer* (**Capa 3**) del [[Modelo OSI - OSI Model]] controla el intercambio de paquetes de datos, ya que estos no pueden enrutarse directamente al receptor y, por lo tanto, deben contar con nodos de enrutamiento. Luego, los paquetes de datos se transfieren de un nodo a otro hasta que alcanzan su destino. Para implementar esto, la capa de red identifica los nodos de red individuales y el control del flujo de datos. Al enviar los paquetes, se evalúan las direcciones y los datos se enrutan a través de la red de un nodo a otro. Normalmente no se procesan los datos en las capas superiores a L3 en los nodos. En base a las direcciones se realiza el enrutamiento y la construcción de tablas de enrutamiento.

Basicamente, la capa de red es responsable de las siguientes funciones:

- **Logical Addressing / Direccionamiento lógico**.
- **Routing / Ruteo**.

Los protocolos de definen en cada capa del [[Modelo OSI - OSI Model]], y estos protocolos representan una coleccion de reglas para la comunicación respectiva en la capa. Son transparentes para los protocolos de las capas superiores o inferiores. Algunos protocolos cumplen tareas de varias capas y se extienden a dos o más capas. Los protocolos más utilizados en esta capa son:

- **IPv4** / **IPv6**
- **IPsec**
- **ICMP**
- **IGMP**
- **RIP**
- **OSPF**

Garantizan el enrutamiento de paquetes desde el origen al destino dentro o fuera de una subred. Estas dos subredes pueden tener diferentes esquemas de direccionamiento o tipos de direccionamiento incompatibles. En ambos casos la transmisión de datos recorre en cada caso toda la red de comunicación e incluye un enrutamiento entre los nodos de la red. Dado que la comunicacioón directa entre el remitente y el receptor no siempre es posible debido a las diferentes subredes, los paquetes deben reenviarse desde nodos (enrutadores) que se encuentran en el camino. Los paquetes reenviados no llegan a las capas superiores, sino que se les asigna un nuevo destino intermedio y se envían al siguiente nodo.
ok