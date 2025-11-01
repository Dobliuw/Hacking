# Bibliotecas **threading** y **multiprocessing**

Las biblitoecas *threading* y *multiprocessing* en Python son herramientas esenciales para la programación concurrente y paralela. Proporcionan mecanismos para ejecutar múltiples tareas simultáneamente, aprovechando mejor los recursos del sistema. 
## Biblioteca threading

**Threading** es una biblioteca para la programación concurrente que permite a los programas ejecutar múltiples *hilos* de ejecución al mismo tiempo. Los hilos son entidades más ligeras que los procesos, comparten el mismo espacio de memoria y son ideales para tareas que requieren poco procesamiento o que están limitadas por E/S.

- **Uso Principal**: Ideal para tareas que no son intensivas en CPU o que esperan recursos (como E/S de red o de archivos).
- **Ventajas**: Bajo costo de creación y cambio de contexto, compartición eficiente de memoria y recursos entre hilos.
- **Desventajas**: Limitada por el Global Interpreter Lock (GIL) en CPython, que previene la ejecución de múltiples hilos de Python al mismo tiempo en un solo proceso.

Ejemplo:
```python
import requests, threading, time

domains = ["https://google.es", "https://wikipedia.org", "https://instagram.com", "https://facebook.com", "https://yahoo.com"]

def wget_without_threads():
	start_time = time.time()

	for url in domains:
		response = requests.get(url)
		print(f"\n[+] DOMAIN [{url}]: {len(response.content)} bytes.")

	end_time = time.time()
	print(f"\n\t[i] Time transcurred: {round(end_time - start_time,2)} s")


def make_wget(url):
	response = requests.get(url)
	print(f"\n[+] DOMAIN [{url}]: {len(response.content)} bytes.")


def wget_with_threads():
	start_time = time.time()

	threads = []
	for url in domains:
		thread = threading.Thread(target=make_wget, args=(url,))
		thread.start()

		threads.append(thread)

	for thread in threads:
		thread.join()

	end_time = time.time()
	print(f"\n\t[i] Time transcurred: {round(end_time - start_time,2)} s\n\n")


if __name__ == "__main__":
	print("\n\t[i] Initializing wgets without threads:")
	wget_without_threads()
	print("\n\t[i] Initializing wgets with threads:")
	wget_with_threads()
```

Tras ejecutar este script podremos comparar en tiempo real como se realizan las peticiones, sin hilos se realizan de manera consecutiva mientras que haciendo uso de estos se realizan de forma simultanea, arrojando como resultado: 

![[threading_python.png]]
## Biblioteca multiprocessing

**Multiprocessing**, por otro lado, se enfoca en la creación de procesos. Cada proceso en multprocessing tiene su propio espacio de memoria. Esto significa que pueden ejecutarse en paralelo real en sistemas con múltiples núcleos de CPU, superando la limitación del GIL.

- **Uso Principal**: Ideal para tareas intensivas en CPU que requieren paralelismo real.
- **Ventajas**: Capacidad para realizar cálculos intensivos en paralelo, aprovechando múltiples núcleos de CPU.
- **Desventajas**: Mayor costo en recursos y complejidad en la comunicación entre procesos debido a espacios de memoria separados.
## Diferencias Clave

- **Modelo de Ejecución**: ‘**threading**‘ ejecuta hilos en un solo proceso compartiendo el mismo espacio de memoria, mientras ‘**multiprocessing**‘ ejecuta múltiples procesos con memoria independiente.
- **Uso de CPU**: ‘**multiprocessing**‘ es más adecuado para tareas que requieren mucho cálculo y pueden beneficiarse de múltiples núcleos de CPU, mientras que ‘**threading**‘ es mejor para tareas limitadas por E/S.
- **Global Interpreter Lock (GIL)**: ‘**threading**‘ está limitado por el GIL en CPython, lo que restringe la ejecución en paralelo de hilos, mientras que ‘**multiprocessing**‘ no tiene esta limitación.
- **Gestión de Recursos**: ‘**threading**‘ es más eficiente en términos de memoria y creación de hilos, pero ‘**multiprocessing**‘ es más eficaz para tareas aisladas y seguras en cuanto a datos.

Ejemplo:
```python
import requests, time, multiprocessing

domains = ["https://google.es", "https://wikipedia.org", "https://instagram.com", "https://facebook.com", "https://yahoo.com"]

def wget_without_processes():
	start_time = time.time()

	for url in domains:
		response = requests.get(url)
		print(f"\n[+] DOMAIN [{url}]: {len(response.content)} bytes.")

	end_time = time.time()
	print(f"\n\t[i] Time transcurred: {round(end_time - start_time,2)} s")


def make_wget(url):
	response = requests.get(url)
	print(f"\n[+] DOMAIN [{url}]: {len(response.content)} bytes.")


def wget_with_processes():
	start_time = time.time()

	processes = []
	for url in domains:
		process = multiprocessing.Process(target=make_wget, args=(url,))
		process.start()

		processes.append(process)

	for process in processes:
		process.join()

	end_time = time.time()
	print(f"\n\t[i] Time transcurred: {round(end_time - start_time,2)} s\n\n")


if __name__ == "__main__":
	print("\n\t[i] Initializing wgets without multiple processes:")
	wget_without_processes()
	print("\n\t[i] Initializing wgets with multiple processes:")
	wget_with_processes()
```

Tras ejecutar este script podremos comparar en tiempo real como se realizan las peticiones, sin el manejo de múltiples procesos se realizan de manera consecutiva mientras que haciendo uso de estos se realizan de forma simultanea, arrojando como resultado: 

![[multiprocessing_python.png]]

También podemos ver con comandos como `ps -faux` los procesos en tiempo real, de esta manera podremos visualizar que en el momento que comienza la ejecución del scrip con el apartado de **multiprocessing** se desprenderan subprocesos del procesos principal de ejecución: 

![[multiprocessing_python_subprocesses.png]]