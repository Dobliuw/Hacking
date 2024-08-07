----
- Tags: #tecnologías
-----
# Protocolos TCP y UDP
Los protocolos [[0. TCP]] y [[0. UDP]] son fundamentales en la comunicación de red, y la librería ‘**socket**‘ en Python proporciona las herramientas necesarias para interactuar con ellos. Aquí tienes una descripción detallada de ambos protocolos y el uso de ‘**socket**‘:

----
# Librería **socket** en Python
###### ¿ Que es un *socket*? 

Un socket es una interfaz de programación de aplicaciones (API) que proporciona una bastracción para la comunicación entre procesos a través de una red, ya sean en la misma máquna o entre máquinas diferentes. Es una forma de establecer conexiones bidireccionales entre porgramas.
###### Librería *socket* en Python

La librería ‘**socket**‘ en Python es una herramienta esencial para la programación de comunicaciones en red. Permite a los desarrolladores crear aplicaciones que pueden enviar y recibir datos a través de la red, ya sea en una red local o a través de Internet. Aquí tienes una visión general de la librería ‘**socket**‘:

- **Creación de sockets**: La librería ‘**socket**‘ proporciona clases y funciones para crear sockets, que son puntos finales de comunicación. Puedes crear sockets tanto para el protocolo TCP (Transmission Control Protocol) como para UDP (User Datagram Protocol).
- **Conexiones TCP**: Puedes utilizar ‘**socket**‘ para establecer conexiones TCP, que son conexiones confiables y orientadas a la conexión. Esto es útil para aplicaciones que requieren transferencia de datos confiable, como la transmisión de archivos o la comunicación cliente-servidor.
- **Comunicación UDP**: La librería ‘**socket**‘ también admite la comunicación mediante UDP, que es un protocolo de envío de mensajes sin conexión. Es adecuado para aplicaciones que necesitan una comunicación rápida y eficiente, como juegos en línea o aplicaciones de transmisión de video en tiempo real.
- **Funciones de envío y recepción**: Puedes utilizar métodos como ‘**send()**‘ y ‘**recv()**‘ para enviar y recibir datos a través de sockets. Esto te permite transferir información entre dispositivos de manera eficiente.
- **Gestión de conexiones**: La librería ‘**socket**‘ incluye métodos como ‘**bind()**‘ para asociar un socket a una dirección y puerto específicos, y ‘**listen()**‘ para poner un socket en modo de escucha, lo que le permite aceptar conexiones entrantes.
- **Conexiones cliente-servidor**: Con ‘**socket**‘, puedes crear aplicaciones cliente-servidor, donde un programa actúa como servidor esperando conexiones entrantes y otro actúa como cliente para conectarse al servidor.

Ejemplo server en python con IPv4 y TCP:
```python
#!/usr/bin/python3
import socket, signal, sys

# Ctrl + C

def ctrl_c(sig, frame):
	print("\n\n\t[!] Quiting...\n")
	server.close()
	sys.exit(1)

signal.signal(signal.SIGINT, ctrl_c)

# Global Vars

HOST = '127.0.0.1'
PORT = 4343

# Main Chat

def start_chat_server(conn):

	with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server:
	server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)

		conn.bind((HOST, PORT))
		conn.listen(1)
		print(f"\n\t[+] Server listening on {HOST}:{PORT}")
		client, addr = conn.accept()
		print(f"\n\t[i] New client connected: {addr[0]}:{addr[1]}")

		while True:
			message = client.recv(1024).decode().strip()
			print(f"\n{addr[0]}:{addr[1]} --> {message}")
			message_to_send = input("\nMessage to send: ")
			client.send(message_to_send.encode('utf-8'))


if __name__ == "__main__":
	start_chat_server(server)
```

Ejemplo cliente en python con IPv4 y TCP: 
```python
#!/usr/bin/python3
import signal, socket, sys

# Ctrl + c

def ctrl_c(sig, frame):
	print("\n\n\t[!] Quiting...\n\n")
	sys.exit(1)

signal.signal(signal.SIGINT, ctrl_c)

# Connect to server (Client)

def connect_to_chat(host, port):

	with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server:
		server.connect((host, port))
		print(f"\n\t[!] Connected to {host}:{port}.")

		while True:
			message_to_send = input("\nMessage to send: ")
			server.send(message_to_send.encode('utf-8'))
			message = server.recv(1024).decode().strip()
			print(f"\nServer --> {message}")


if __name__ == "__main__":
	if len(sys.argv) == 3:
		host, port = sys.argv[1], int(sys.argv[2])
		connect_to_chat(host, port)
	else:
		print("\n\n\t[!] Execution: python3 %s {host} {port}\n\n" % sys.argv[0])
		sys.exit(1)
```

Ejemplo server en python con IPv4 y UDP:
```python
import socket, signal, sys

def ctrl_c(sig, frame):
	print("\n\n\t[!] Quiting...\n")
	sys.exit(1)

signal.signal(signal.SIGINT, ctrl_c)

# UPD Server

def start_udp_server():

	host = "localhost"
	port = 1234

	# UDP
	with socket.socket(socket.AF_INET, socket.sock_DGRAM) as server:
		server.bind((host, port))
		pirnt(f"\n\t[i] Server listenning on: {host}:{port} (UDP)")

		while True:
			data, addr = server.recvfrom(1024)
			print(f"\n\t[i] Message recived:\n{data.decode()}")
			print(f"\n\n\t[i] Client information:\n\t+ IP: {addr[0]}\n+ HOST: {addr[1]}")

if __name__ == "__main__":
	start_udp_server()
```

Ejemplo cliente en python con IPv4 y UDP:
```python
import socket, signal, sys

# Ctrl C

def ctrl_c(sig, frame):
	print("\n\n\t[!] Quiting...\n")
	sys.exit(1)

signal.signal(signal.SIGINT, ctrl_c)

# Server

def start_udp_client():

	host = "localhost"
	port = 4343

	with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as server:
		message = "Message to send".encode("utf-8")
		server.sendto(message, (host, port))

if __name__ == "__main__":
	start_udp_client()
```

En estos ejemplos, estamos montando servidores y clientes por IPv4 haciendo uso de los protocolos TCP y UDP, pero algo a tener en cuenta es que existe una cola de espera a la hora de llevar a cabo estas conexiones, es decir, si el servidor esta en escucha y 4 clientes se conectan de manera simultanea, 3 clientes quedaran en espera mientras el servidor establece conexión con el primer cliente, para poder permitir múltiples conexiones podemos hacer uso de hilos, con la librería **threading**.

----
# Librería **threading**

La función ‘**setsockopt**‘ en la programación de redes juega un papel crucial al permitir a los desarrolladores ajustar y controlar varios aspectos de los sockets. Los sockets son fundamentales en la comunicación de red, proporcionando un punto final para el envío y recepción de datos en una red.

#### Niveles en setsockopt

Cuando utilizas ‘setsockopt’, puedes especificar diferentes niveles de configuración, que determinan el ámbito y la aplicación de las opciones que estableces:

- **Nivel de Socket (SOL_SOCKET)**: Este nivel afecta a las opciones aplicables a todos los tipos de sockets, independientemente del protocolo que estén utilizando. Las opciones en este nivel controlan aspectos generales del comportamiento del socket, como el tiempo de espera, el tamaño del buffer, y el reuso de direcciones y puertos.
- **Nivel de Protocolo**: Este nivel permite configurar opciones específicas para un protocolo de red en particular, como TCP o UDP. Por ejemplo, puedes ajustar opciones relacionadas con la calidad del servicio, la forma en que se manejan los paquetes de datos, o características específicas de un protocolo.
#### socket.SOL_SOCKET

‘**socket.SOL_SOCKET**‘ es una constante en muchos lenguajes de programación que se usa con ‘setsockopt’ para indicar que las opciones que se van a ajustar son a nivel de socket. Esto significa que las opciones aplicadas en este nivel afectarán a todas las operaciones de red realizadas a través del socket, sin importar el protocolo de transporte específico (como TCP o UDP) que esté utilizando.
#### socket.SO_REUSEADDR

‘**socket.SO_REUSEADDR**‘ es otra opción comúnmente utilizada en setsockopt. Esta opción es muy útil en el desarrollo de aplicaciones de red. Lo que hace es permitir que un socket se enlace a un puerto que todavía está siendo utilizado por un socket que ya no está activo. Esto es particularmente útil en situaciones donde un servidor se reinicia y sus sockets aún están en un estado de “espera de cierre” (**TIME_WAIT**), lo que podría impedir que el servidor se vuelva a enlazar al mismo puerto.

Al establecer ‘**SO_REUSEADDR**‘, el sistema operativo permite reutilizar el puerto inmediatamente, lo que facilita la reanudación rápida de los servicios del servidor.

En resumen, ‘**setsockopt**‘ con diferentes niveles y opciones, como ‘**SOL_SOCKET**‘ y ‘**SO_REUSEADDR**‘, proporciona una flexibilidad significativa en la configuración de sockets para una comunicación de red eficiente y efectiva.

Ejemplo de servidor que acepta múltiples conexiones y usa socket.setsockopt:
```python
import socket, threading

class ClientThread(threading.Thread):
	def __init__(self, client, addr):
		super().__init__()
		self.client = client
		self.addr = addr

		print(f"\n[i] New client: {addr[0]}:{addr[1]}")

	def run(self):
		message = ""
		while True:
			message = self.client.recv(1024).decode()
			print(message)
			if message.strip() == "bye":
				break

			print(f"\n[+] Message recived from {self.addr[0]}:{self.addr[1]}: {message}")
			self.client.send(message.encode())

		print(f"\n\t[!] Client {self.addr[0]}:{self.addr[1]} disconected\n")
		self.client.close()

HOST = "localhost"
PORT = 4343

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server:
	server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1) # TIME_WAIT
	server.bind((HOST, PORT))

	print(f"\n[+] Listenning on {HOST}:{PORT}")

	while True:
		server.listen()
		client, addr = server.accept()
		new_thread = ClientThread(client, addr)
		new_thread.start()
```