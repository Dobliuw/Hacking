----
- Tags: #tecnologías
-----
# Modulo **requests** 

La biblioteca **requests** en Python es una de las herramientas más populares y poderosas para realizar solicitudes HTTP. Su diseño es intuitivo y fácil de usar, lo que la hace una opción preferida para interactuiar con APIs y servicios web.
###### Características Principales

- **Simplicidad y Facilidad de Uso**: Con requests, enviar solicitudes GET, POST, PUT, DELETE, entre otras, se puede realizar en pocas líneas de código. Su sintaxis es clara y concisa.
- **Gestión de Parámetros URL**: Permite manejar parámetros de consulta y cuerpos de solicitud con facilidad, automatizando la codificación de URL.
- **Manejo de Respuestas**: ‘**requests**‘ facilita la interpretación de respuestas HTTP, proporcionando un objeto de respuesta que incluye el contenido, el estado, los encabezados, y más.
- **Soporte para Autenticaciones**: Ofrece soporte integrado para diferentes formas de autenticación, incluyendo autenticación básica, digest, y OAuth.
- **Manejo de Sesiones y Cookies**: Permite mantener sesiones y gestionar cookies, lo cual es útil para interactuar con sitios web que requieren autenticación o mantienen estado.
- **Soporte para SSL**: ‘**requests**‘ maneja SSL (Secure Sockets Layer) y TLS (Transport Layer Security), permitiendo realizar solicitudes seguras a sitios HTTPS.
- **Manejo de Excepciones y Errores**: Proporciona métodos para manejar y reportar errores de red y HTTP de manera efectiva.
-----
# Uso de *Requests*

La biblioteca se utiliza ampliamente para interactucar con APIs RESTful, automatizar interacciones con sitios web, y en tareas de scraping web. Sus capacidades para manejar solicitudes complejas y sus características de seguridad la hacen ideal para un amplia gama de aplicaciones, desde scripts simles hasta sistemas empresariales complejos.

Ejemplos:
```python
import requests

# Default get
response = requests.get("url")

# Status code
print(response.status_code)

# Font code
print(response.text)

# Authentication
requests.get('url', auth=('user', 'pass'))

# Giving params
params_dict = {'key1': 'value1', 'key2', 'value2'}
new_response = requests.get("url", params=params_dict)

# Giving payload
payload_dict = {'key1': 'value1', 'key2', 'value2'}
new_response_2 = requests.post("url", data=payload_dict)

# Modifying headers
header = {'User-Agent': 'Mozilla 3.0 dobliuw gvng'}
new_response_3 = resquests.get("url", headers=header)
print(new_response_3.request.header)

# Modifying cookies
cookies = dict(token="dobliuwcookie") # {"token": "dobliuwcookie"}
requests.get("url", cookies=cookies)

# Sending files
file_to_upload = {"file": open("my_file", "r")}
requests.post("url", files=file_to_upload)

# Track all urls
track_response = requests.get("url")
print(track_response.history)

# Block redirects
requests.get("url", allow_redirects=False)

# Disable auto signed SSL Certificates error (https)
requests.packages.urllib3.disable_warnings(requests.packages.urllib3.exceptions.InsecureRequestWarning)
requests.get("url", verify=False)

# Handling exceptions
try:
	new_response_4 = requests.get('url', timeout=1)
	new_response_4.raise_for_status()
	
except requests.Timeout: # Handle timeout
	print("The website did not response.")
	
except requests.HTTPError: # Handle HTTP error
	print("The website has an error.")

except requests.RequestException: # Handle all requests exceptions
	print("An error ocurred")

```

Ahora, en caso de tener que tramitar múltiples peticiones para poder ejecutar lo que nos interesa, supongamos que debemos loguearnos en un panel para posteriormente dirigirnos a un apartado de la url y realizar la acción final, podríamos jugar con **sesiones**, de esta manera declarariamos lo siguiente:

```python
import requests

s = requests.session()
response = s.get("url")
s.verify = False 

############################
import requests

with requests.Session() as s:
	s.auth = ("user", "pass")
	response1 = s.get("url")
	response2 = s.get("url2")

```

De manera que una vez tengamos la sessión declarada en una variable, en este caso la variable **s**, podríamos hacer uso de esta session para tramitar todas las peticiones que nos interese tramitar. 

-----
# Biblioteca URLlib3

La biblioteca **urllib3** de Python es ampliamente utilizada para realizar solicutides HTTP y HTTPS. Es conocida por su robustez y sus numerosas características, que la hacen una herrmaienta versátil para una variedad de aplicaciones de red. A continuación, se presenta una descripción detallada de **urllib3** y sus capacidades.

- **Gestión de Pool de Conexiones**: Una de las características más destacadas de ‘**urllib3**‘ es su manejo de pools de conexiones, lo que permite reutilizar y mantener conexiones abiertas. Esto es eficiente en términos de rendimiento, especialmente cuando se hacen múltiples solicitudes al mismo host.
- **Soporte para Solicitudes HTTP y HTTPS**: ‘**urllib3**‘ ofrece un soporte sólido para realizar solicitudes tanto HTTP como HTTPS, brindando la flexibilidad necesaria para trabajar con una variedad de servicios web.
- **Reintentos Automáticos y Redirecciones**: Viene con un sistema incorporado para manejar reintentos automáticos y redirecciones, lo cual es esencial para mantener la robustez de las aplicaciones en entornos de red inestables.
- **Manejo de Diferentes Tipos de Autenticación**: Proporciona soporte para varios esquemas de autenticación, incluyendo la autenticación básica y digest, lo que la hace apta para interactuar con una amplia gama de APIs y servicios web.
- **Soporte para Características Avanzadas del HTTP**: Incluye soporte para características como la compresión de contenido, el streaming de solicitudes y respuestas, y la manipulación de cookies, ofreciendo así un control detallado sobre las operaciones de red.
- **Gestión de SSL/TLS**: ‘**urllib3**‘ tiene capacidades avanzadas para manejar la seguridad SSL/TLS, incluyendo la posibilidad de trabajar con certificados personalizados y la verificación de la conexión segura.
- **Tratamiento de Excepciones y Errores**: La biblioteca maneja de manera eficiente las excepciones y errores, permitiendo a los desarrolladores gestionar situaciones como tiempos de espera, conexiones fallidas y errores de protocolo.
- -----
# Uso de *urllib3*

Esta librería se utiliza en una variedad de contextos, desde scraping web y automatización de tareas, hasta la construcción de clientes para interactucar conAPIs complejas. Su capacidad para manejar conexiones de manera eficiente y segura la hace adecuada para aplicaciones que requieren un alto grado de interacción de red, así como para escenarios donde el rendimiento y la fiabilidad son cruciales.

Ejemplos: 
```python
import urllib3

http = urllib3.PoolManager() # Controlador de conexiones

response = http.request('GET', 'url')
print(response.data) # Respuesta en formato bytes
print(response.data.decode())

# Send encoded data in body
encoded_data = json.dumps({'atributo': 'valor'}).encode()
http.request('GET', 'url', body=encoded_data)

# Send un-encoded data in body
http.request('GET', 'url', fields={'atributo':'valor'})

# Modifying headers
http.request('POST', 'url', headers={'Content-Type': 'application/json'})

# Modifying redirects
http.request('GET', 'url', redirect=False)

# Track redirects 
new_response = http.request('POST', 'url', redirect=False)
print(new_response.get_redirect_location()) # New tryin redirect url

# Disable auto signed SSL Certificates error (https)
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
http = urlib3.PoolManager(cert_reqs='CERT_NONE')
```

