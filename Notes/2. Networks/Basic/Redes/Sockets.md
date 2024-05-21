# Sockets

Los **sockets** son puntos finales (*endpoints*) de una comunicación bidireccional entre dos nodos de una red. Son una abstracción que permite la comunicación a través de una red, independientemente del protocolo subyacente (TCP, UDP, etc).
###### Sockets types

**Stream Sockets** (**Sockets de flujo**):
- *Protocolo subyacente*: TCP.
- *Características*: Orientado a la conexión, garantiza la entrega de datos en el mismo orden en que se envían, es decir que es confiable.
- *Uso típico*: COmunicación cliente-servidor donde se enecesita confiabilidad, como HTTP, FPT, etc.

**Datagram Sockets** (**Sockets de datagrama**):
- *Protoclo subyacente*: UDP.
- *Características*: No orientado a conexión, no garantiza entrega ni orden, menos sobrecarga que TCP.
- *Uso típico*: APlicaciones donde la velocidad es crítica y cierta pérdida de datos es aceptable, como la transmisión de video en tiempo real, juegos en línea, etc.

**Direcciones y Puertos**:
- *IP Address*: Identifcia un dispisitivo en la red.
- *Port*: Identifica una aplicación o proceso específico en el dispositivo.
- *Socket Address*: Combinación de una dirección IP y un puerto.

---
# PoC

Por ejemplo podríamos hacer uso de lenguajes como *Python* para llevar a cabo el uso de sockets creando un cliente y un servidor con librerias como **socket**, o incluso podríamos hacer uso de la herramienta **tor** (Proyecto que utiliza nodos proxies utilizados para anonimizar el tráfico) la cual crea un *socks5* y haciendo uso de librerías como **socks** podríamos crear un socket que se conecte al proxy proporcionado por tor.

```python
import socket, socks

# Configure SOCKS5 proxy to use TOR
socket.set_default_proxy(socks.SOCKS5, "{host_proxy_tor_ip}", {host_proxy_tor_port})
socket.socket = socks.socksocket

# Create a socket to use proxy TOR
try:
	s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
	s.connect(("{any_server_web}", {any_server_port})) # Connection throught TOR
	s.sendall(b"GET / HTTP/1.1\r\nHost: {any_server_web}\r\n\r\n")
	response = s.recv(4096)
	print(response.decode())
	s.close()
except Exception as e:
	print(f"An error ocurred: {e}")
```