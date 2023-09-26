- Tags: #teoria #practica #blue 
- ------
# Phishing

Phshing es un a forma de ciberataque en la que los atacantes intentean engañar a las personas para reveln información confidencial, como contraseñas, núimeros de tarjeta de cŕedito, información bancaria u otra información personal sensible. Esto lo hacen haciéndose pasar por entidades bancarios, legítimas, servicios de correo electrónico, etc.
Los atacantes suelen utilizar correos electrónicos, mensajes de texto, llamadas telefónicas u otros métodos de comunicación para enviar mensjaes fraudulentos a las víctimas.

-----
# Análisis 
##### **\[+]** Se envió del servidor SMTP correcto? 
Cuando recibimos un mail desde un determinado remitente, supongamos **dobliuw\@dobliuw.com**, lo primero que podemos hacer es verificar en páginas como [MX toolbox](https://mxtoolbox.com/SuperTool.aspx) (Plataforma en línea que ofrece una variedad de herramientas y servicios relacionados con la gestión de servidores de correo electrónico y la seguridad en línea) para buscar el dominio **dobliuw.com**, la IP obtenida de estab búsqueda será comparada con la IP obtenida del mail que recibimos.
Si las IP *no coinciden*, es una señal de que el email pudo ser *spoofed* (Se falsifico o imito). 

##### **\[+]** Los datos de *From* y *Return-Path / Reply-To* coinciden?
El campo **From** muestra la dirección de correo electrónico del remitente tal como aparece en el correo recibido. En un correo legítimo, la dirección en el campo *From* debería coincidir con la idetndidad del remitente real.
El campo **Return-Path** especifica la dirección de retorno a la que deben enviarse los rebotes o mensajes no entregados, mientras que **Reply-To** indiica la dirección de correo electrónico al a que se debe responder si el destinatario elige responder al correo electrónico.
Es importante que estos campos sean los mismos, esto aumenta la autenticidad y la seguridad del correo, estos campos deben tener las mismas direcciones o, al menos, ser coherentes. **IMPORTANTE** tener en cuenta que si bein es buena práctica de seguridad tener en cuenta que estos datos coincidan, *no todos* los correos *legítimos* cumpliran estrictamente esta regla.

##### **\[+]** Revisar la *IP* obtenida en el correo.
Revisar la IP obtenida en el correo puede ayudarnos a verificar si el correo aumenta las señales de sospecha o de legitimidad, para esto podemos usar recursos como [Alien Vault](https://otx.alienvault.com/),  [AbuseIPDb](https://otx.alienvault.com/) y [Virus Total](https://www.virustotal.com) .

##### **\[+]** Errores de gramatica?
En caso de que el mail cuente con errores de gramatica o errores en el correo, ya sea de la posición de la persona que se esta intentando suplantar o cualquier tipo de equivocación que podamos detectar de cara al correo electrónico son aspectos que aumentan la deconfianza del mismo.

##### **\[+]** Archivos adjuntos sospechosos.
Los archivos adjuntos en un correo electrónico legítimo generalmente se mencionan dentro del cuerpo. El remitente puede decir por ejemplo: "Adjunto el informe". Esto facilita la verificación del archivo adjunto porque su nombre debe correlacionarse con lo mencionado en el mensaje.
En un correo electrónico de phishing, es posible que el archivo adjunto no tenga anda que ver con el contenido del cuerpo de correo electrónico. También puede ser innecesario que se adjunte el mismo, por ejemplo, un correo electrónico sobre un informe pero con un archvio adjunto que contiene instrucciones sobre cómo restablecer la contraseña.

##### **\[+]** OSINT de archivos adjuntos
En caso de contar un mail con archivos adjuntos, puede ser buena practica de cara al **análisis de phishing** la descarga de este archivo en un entorno aislado (Como un sandbox) para el análisis del mismo, la extracción del hash MD5 para así analizarlo posteriormente con OSINT en páginas como [Virus Total](https://www.virustotal.com) .