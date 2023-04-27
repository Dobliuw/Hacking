----
- Tags: #teoria #ataques #basico #practica
---

# ¿ Que es un **CSTI** ? 

### El **Client-Side Template Injection** ( **CSTI** ) es una vulnerabilidad de seguridad en la que un atacante puede inyectar código malicioso en una *plantilla de cliente*, que se ejecuta en el **navegador** del usuario en lugar del servidor. 

### A diferencia del [[SSTI - (Server-Side Template Injection)]], en el que la plantilla de servidor se ejecuta en el servidor y es responsable de generar el contenido dinámico, en el **CSTI**, la plantilla de cliente se ejecuta en el navegador del usuario y se utiliza para generar contenido dinámico en el lado del cliente. 

### Los atacantes puede aprovechar una vulnerabilidad de **CSTI** para inyectar código malicioso en una platinlla de cliente, lo que les permite ejecutar comandos en el navegador del usuario y obtener acceso no autorizado a la aplicación web y a los datos sensibles. 

### Una deriavión común de un ataque de **CSTI** es aprovecharlo para realizar un ataque de [[XSS  - ( Cross-Site Scripting )]]. 

### Una vez que un atacante ha inyectado código malicioso en la plantilla del cliente, puede manipular los datos que se muestran al usuario, lo que le permite ejecutar código JavaScrip en el navegador del usuario. A través de este código malicioso, el atacante puede intentar robar la cookie de sesión del usuario, lo que le permitiría obtener acceso no autorizado a la cuenta del usuario y realizar acciones maliciosas en su nombre. 

----

# Explotación 

