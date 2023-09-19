---

---
------------
- Tags: #teoria #blue #phishing
----------
# Phishing
### Es una forma de ciberataque en la que los delincuentes intentan engañar a las personas para que revelen infromación confidencial, como contraseñas, números de tarje de crédito o información personal. Los atacantes suelen hacerse pasar por una entidad confiable, como un banco, una empresa, o una organización, con el fin de engañar a las víctimas.

----
# Protocolo SPF
### **SPF** (**S**ender **P**olicy **F**ramework) es un **protocolo de autenticacion de correos** que permite al propietario de un dominio (Por ejemplo, **dobliuw.com**), especificar qué servidores de correo utilizará para el envío de e-mail desde ese dominio. El protocolo permite también que el receptor pueda confirmar que el srvidor que envía correos es legítimo, evitando que esos e-mails sean considerados como **spam** o **correos falsos**. 

## ¿ Como funciona ?

- ### **Publicación de Registros SPF**: El propietario de un dominio publica un registro SPF en el registro DNS de us dominio. Esrte registro SPF (Archivo .txt) contiene información sobre qué servidores de correo electrónico están autorizados para enviar correos electrónicos en nombre de ese dominio.
- ### **Envío de Correos Electrónicos**:  Cuando el remitente envía un correo electrónico, el servidor de correo de destino verifica el registro SPF del dominio del remitente.
- ### **Verificación SPF**: El servidor de destino consulta el registro SPF para determinar qué servidores de corre electrónico están autorizados para enviar correos electrónicos en nombre de ese dominio. Luego, compara la dirección IP del servidor de correo que envió el mensaje con las direcciones IP permitidas en el registro SPF. 
- ### **Acciones basadas en SPF**: Dependiendo del resultado de la verificación SPF, el servidor de destino toma una de las siguientes acciones: **Pass, Fail**. 

![[SPF_Protocol.png]]

------
# Protocolo DKIM
### El protocolo [DKIM](https://dkim.org/) (**Domain Keys Identified Mail**) es un protocolo que permite asociar un nombre de dominio a un mensaje mediante técnicas criptográficas. Al enviar un correo electrónico se incluye una **firma** o **huella digital** en su cabecera. Se trata de una marca única e intrasnferible que es muy díficil de falsificar. De esta forma, cuando el destinatario recibe un mensaje verifica la firma incluida en la cabecera, validando el mensaje y su procedencia. 

## ¿ Como funciona ? 

- ### **Generación del Par de Claves DKIM**: Para habilitar DKIM, el propietario del dominio debe generar un par de claves DKIM (Una clave privada y una clave pública). La clave privada se mantendrá en secreto y se usará para firmar los correos electrónicos salientes, mientras que la clave pública se publicará en el registro DNS del dominio.
- ### **Configuración del Selector DKIM**: El remitente debe elegir un "selector" DKIM, que es una etiqueta que se utiliza en el registro DNS para indicar qué conjunto de claves DKIM se utilizará para firmar los correos. El selector se incluye en el encabeado DKIM-Signature del correo electrónico.
- ### **Firmar del Correo Electrónico**: Cuando el remitente envía un correo, el servidor de correo del remitente utiliza la clave privada DKIM para calcular una firma digital que abarca todo el contenido del mensaje, incluyendo el encabezado y el cuerpo.
- ### **Inclusión de la Firma DKIM en el Encabezado**: La firma DKIM se agrega como un campo DKIM-Signature en el encabezado del correo electrónico. Esta firma contiene información sobre la clave utilizada, el selector, y la firma digitial del contenido del correo.
- ### **Envío de Correo Electrónico**: El correo se envía al destinatario.
- ### **Verificación en el Servidor del Destinatario**: Cuando el servidor de correo recibe el crreo electrónico, consulta el registro DNS del dominio del remitente para obtener la clave pública correspondiente al selector indicado en la fimra DKIM.
- ### **Verificación de la Firma**: El servidor del destinatario utiliza la clave pública obtenida del DNS para verificar la firma DKIM en el correo electrónico. Si la firma es válida y coincide con el contenido del mensaje, se considera auténtico y que no ha sido alterado en tránsito.

![[DKIM_protocol.png]]

-----
# DMARC
### DMARC (**Domain-based Message Authentication, Reporting and Conformance**) es un **estándar de autenticación** de correos electrónicos que verifica, tanto SPF, como DKIM permitiendo, además, a los propietarios de dominios dar indicaciones a los preveedores de correo electrónico (**ISP**), para actuar en caso de que detecte un ataque de suplantación o modificación de corres. De esta forma, aumenta nuestra capacidad de proteger un dominio ante un uso no autorizado o una suplantación de indentidad. 

## ¿ Como funciona ? 

- ### **Publicación de Políticas DMARC**: El propietario del dominio publica una política DMARC en el registro DNS de su dominio. Esta política especifica cómo los correos electrónicos que afirma ser del dominio deben ser tratados por los receptores de correo.
- ### **Recepción de Correo Electrónico**: Cuando un receptor de correo electrónico recibe un mensaje de correo electrónico, verifica si el dominio del remitente tiene una política DMARC publicada.
- ### **Verificación SPF y DKIM**: El receptor también verifica si el mensaje cumple con las políticas SPF y DKIM del dominio del remitente. SPF verifica que el servidor de correo es autorizado para enviar correos en nombre del dominio y DKIM verifica la firma digital del mensaje.
- ### **Acciones basadas en la Política DMARC**: Dependiendo de la política DMARC establecida por el dominio del remitente, el receptor toma una de las siguientes acciones: **Reject, Quarantine o None**.
- ### **Informes y Monitoreo**: DMARC también permite a los propietarios de dominios recibir informes de los receptores sobre cómo se están manejando los correos electrónicos que afirman ser del dominio. Estos informes proporcionan datos que ayudan a los remitente a monitorear y mejorar la autenticación de sus correos electrónicos.
### De cara a la definición de "receptores", nos referimos a: 
- ### Servidores de Correo Electrónico.
- ### Sistemas de Filtrado de Corre.
- ### Proveedores de Servicios de Correo.
- ### Filtros de Spam y Seguridad

![[DMARC_standard.png]]