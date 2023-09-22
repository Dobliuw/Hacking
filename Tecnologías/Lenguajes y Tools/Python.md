----
- Tags: #tecnologías
-----
# Modulo **requests** 

Con el modulo requests que podemos tramitar peticiones http o https, es importante tener encuenta ciertos aspectos. 
En caso de querer tramitar peticiones https podríamos importar el modulo **urllib3** y posterirmente ejecutar un **urllib3.disable_warnings()**. 

```python
import urllib3

urlib3.disable_warnings()
```

Ahora, en caso de tener que tramitar múltiples peticiones para poder ejecutar lo que nos interesa, supongamos que debemos loguearnos en un panel para posteriormente dirigirnos a un apartado de la url y realizar la acción final, podríamos jugar con **sesiones**, de esta manera declarariamos lo siguiente:

```python
import requests

s = requests.session()
s.verify = False 
```

De manera que una vez tengamos la sessión declarada en una variable, en este caso la variable **s**, podríamos hacer uso de esta session para tramitar todas las peticiones que nos interese tramitar. 

```python
s.post("http://127.0.0.1/login", data=login_data)

s.get("http://127.0.0.1/url_post_authentication")
```