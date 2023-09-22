---------------------
-  Tags: #teoria #practica #blue #basico
---------------------
# OWASP

OWASP es un proyecto de código abierto dedicado a determinar y combatir las causas que hacen que el software sea inseguro, esta organización sin fines de lucro se dedica a la seguridad de las aplicaciones web. 

-----
# [OWASP Top 10 API](https://owasp.org/API-Security/editions/2023/en/0x11-t10/)

# #1 Broken Object Level Authorizations
Las API tienden a exponer endpoints que manejan idenficiadores de objetos, creando una amplia superfice de ataque para problemas de **Object Level Access Control**. Se deben considerar comprobaciones de  la autorización a nivel de objeto en cada función que accede a una fuente de datos utilizando un ID del usuario.

## **Como se puede acontecer?**
Manipulando IDs para impersonar a otros usuarios o el acceso a los datos. 

## **Ejemplo**:
- ### Un atacante autenticado como User A puede acceder a la data del User B.
## **Riesgos**:
- ### Puede provocar pérdida de datos, divulgación o manipulación de datos.
## **Prevención**:
- ### Definir políticas de acceso a datos e implementar controles asociados.
- ### Asegurarse de qeu el usuario autenticado esté autorizado a recibir los datos solicitados.
- ### Implementar pruebas autmatizadas para identificar vulnerabilidades BOLA (Broken Object Level Authorization)

----
# #2 Broken Authentication 
Los mecanismos de autenticación a menudo se implementa incorrectamente, lo que permite a los atacantes comprometere tokens de auteticación o explotar fallas e nla implementación para asumir temporal o permanentemente las identidades de otros usuarios. Comprometer la capacidadd e un sistema para identificar al cliente/usario compromete la seguridad de la API en general.

## **Como se puede acontecer?**
Una devil o pobre autenticación.

## **Ejemplo**: 
- ### Requerimientos de controaseñas debiles.
- ### Credential Stuffing (Fuerza Bruta ID/PW).
- ### No captcha/no rate limiting/no lockout.
- ### Información de la autenticación en la URL (Tokens, Credenciales).
- ### Sin validación de la expiración del token.
- ### Almacenamiento inseguro de las contraseñas.
## **Riesgos**: 
- ### Apropiación/Robos de cuenta, de datos o transacciones sin autorización.
## **Prevención**: 
- ### Definir politicas y standars de autenticacion siguiendo las mejores practicas e implementar testeos continuos.

----
# #3 Broken Object Property Level Authorization
Esta categoría combina la vulnerabilidad [Excessive Data Exposure (API3:2019)](https://owasp.org/API-Security/editions/2019/en/0xa3-excessive-data-exposure/) y la vulnerabilidad [Mass Asignment (API6:2019)](https://owasp.org/API-Security/editions/2019/en/0xa6-mass-assignment/), centrándose en la causa pirncipal: La falta de validación de autorización o su implementación incorrecta a nivel de propiedad del objeto, esto conduce a la exposición o manipulación de información por parte de partes no autorizadas.

## **Como se puede acontecer?**
Explotando endpoints leyendo o/y modificando los valores de los objetos.

## **Ejemplo**: 
- ### Un usuario esta capacitado a modificar/setear `account-type=admin`.
- ### Un usuario busca endpoints que retornan datos y detalles excesivos e innecesarios (Nombre, Email, Dirección, ID, etc.).
## **Riesgos**:
- ### Revelar data protegida del usuario.
## **Prevención**:
- ### Asegurarse de que el usuario solo pueda acceder a campos legítimos y permitidos.
- ### Devolver la cantidad mínima de datos requeridos para el caso de uso.

----
# #4 Unrestricted Resource Consumption
Satisfacer las solicitudes de API requiere recursos como ancho de banda de red, CPU, memoria y almacenamiento. Otros recursos, como correos electrónicos/SMS/llamadas telefónicas o validación biométrica, están disponibles a través de integraciones de API proporcionadas por proveedores de servicios y se pagan por solicitud. Los ataques exitosos pueden llevar a una Denegación de Servicio o a un aumento en los costos operativos.

## **Como se puede acontecer?**
La falta de recursos o velocidad limitada.

## **Ejemplo**:
- ### Controles de volumen faltantes o inadecuados (Establecidos demasiado altos).
- ### Tiempos de ejecución.
- ### Memoria máxima asignable.
- ### Número máximo de descriptores de archivos.
- ### Tamaño máximo de carga de archivos.
- ### Operaciones excesivas en una sola solicitud. 
- ### Se devuelven registros excesivos en una sola solicitud.
## **Riesgos**:
- ### DDoS (Ataques de denegación de Servicio).
- ### Recolección de datos.
## **Prevención**:
- ### Implementar controles de tráfico.

----
# #5 Broken Function Level Authorization
Las políticas de control de acceso complejas con diferentes jerarquías, grupos y roles, y una separación poco clara entre funciones administrativas y regulares, tienden a generar fallas en la autorización. Al explotar estos problemas, los atacantes pueden acceder a los recursos de otros usuarios y/o funciones administrativas.
## **Como se puede acontecer?**
Usando funcionalidades de la API para modificar (CREATE, UPDATE, DELETE) recursos de otro usuario o cambiando metodos pasivos (GET) por activos (PUT, DELETE). También puede ser usada para escalar privilegios o 

## **Ejemplo**: 
- ### Remplazando el método GET por PUT.
- ### Modificando parametros de la URL `{"role=admin","account-type=premium"}`.
- ### Eliminando facturas, seteando el saldo a $0 o negativo.
## **Riesgos**:
- ### Acceso a funcionalidades o endpoints restringidos.
- ### Modificación en detalles de las cuentas.
## **Prevención**:
- ### Identificar funciones que expongan capacidades de alta sensibilidad y desarrollar contorles para limitar el acceso.
- ### implementar pruebas continuas para garantizar el comportamiento adecuado.

----
# #6 Unrestricted Access to Sensitive Business Flows
Las APIs vulnerables a este riesgo exponen un flujo de negocio, como comprar un boleto o publicar un comentario, sin tener en cuenta cómo la funcionalidad podría perjudicar al negocio si se utiliza de manera excesiva de manera automatizada. Esto no necesariamente se debe a errores de implementación.

## **Como se puede acontecer?**
Abusando de un flujo de trabajo empresarial legítimo mediante el uso excesivo y automatizado, limitando el tráfico (Los captchas no siempre son efectivos contra el tráfico fraudulento), rotando IPs rapidamente para evitar detecciones, errores lógicos en la aplicación.

## **Ejemplo**: 
- ### Masiva y autmatizadas solicitudes o compra de tickets.
- ### Bonos de alto volumen
## **Riesgos**:
- ### Pérdida de actividad empresarial crítica.
## **Prevención**:
- ### Identificar flujos de trabajo empresariales críticos.
- ### implementar detección y control de tráfico fraudulento.
- ### Configurar y automatizar pruebas del mecanismo de control.

----
# #7 [[SSRF - (Server-Side Request Forgery)]]
Las fallas de [[SSRF - (Server-Side Request Forgery)]] pueden ocurrir cuando una API está obteniendo un recurso remoto sin validar el URI proporcionado por el usuario. Esto permite a un atacante obligar a la aplicación a enviar una solicitud manipulada a un destino inesperado, incluso cuando está protegido por un firewall o una VPN.

## **Como se puede acontecer?**

Explotando inputs de URLS para realizar peticiones a servers 3ros maliciosos.

## **Ejemplo**: 
- ### Puede darse mediante el abuso de un previo [[LFI - (Local File Inclusion)]].
- ### URL maliciosa en un input capaz de realizar peticiones.
- ### Malware descargado desde un sitio malicioso.
## **Riesgos**:
- ### Fuga de información potencial.
- ### Creación de un canal para peticiones maliciosas, acceso de datos u otras actividades fraudulentas.
## **Prevención**:
- ### Validar y sanitizar todas la información solicitada e introducida por el usuario (Inluidos los parámetros de URL).
- ### Asegurarse de que la comunicación sólo sea permitida con dispositivos confiables.
- ### Probar la eficiencia de la validación URL.

---
# #8 Security Misconfiguration
Las APIs y los sistemas que las respaldan suelen tener configuraciones complejas destinadas a hacer que las APIs sean más personalizables. Los ingenieros de software y DevOps pueden pasar por alto estas configuraciones o no seguir las mejores prácticas de seguridad cuando se trata de la configuración, lo que abre la puerta a diferentes tipos de ataques.

## **Como se acontece?**
Falta de protección contra servicios innecesarios, uso de bots para ecaneos, detecciones y explotaciones de configuraciones erróneas.

## **Ejemplo**:
- ### Falta de seguridad.
- ### Permisos configurados incorrectamente.
- ### Falta de parches de seguridad.
- ### Falta de TLS.
- ### Falta de política de CORS o mala configuración de la misma.
## **Riesgos**:
- ### Exposición de datos confidenciales del usuario.
- ### Potencial compromiso total del servidor.
## **Prevención**:
- ### Implementar procedimientos de refuerzo de la seguridad.
- ### Revisar periódicamente las configuraciones.
- ### Implementar pruebas de seguridad continuas y automatizadas.

-----
# #9 Improper Iventory Management
Las APIs tienden a exponer más puntos finales que las aplicaciones web tradicionales, lo que hace que la documentación adecuada y actualizada sea muy importante. Un inventario adecuado de hosts y versiones de API implementadas también es importante para mitigar problemas como versiones de API obsoletas y puntos finales de depuración expuestos.

## **Como se acontece?**

Accediendo no autorizadamenta a APIs viejas, que ya no estan actualizadas o a través de terceros confiables.

## **Ejemplo**:
- ### Versiones antiguas de APIs.
- ### Endpoints sin parches.
- ### Endpoints con requisitos de seguridad  débiles.
- ### Acceso a API a través de terceros.
- ### Documentación vencida o fuera de fecha.
- ### Endpoints innecesariamente expuestos.
## **Riesgos**:
- ### Robo de datos o cuentas.
- ### Exposición de datos confidenciales.
## **Prevención**:
- ### Hacer cumplir una política estricta para la implementación en todas las APIs (En Gateways).
- ### Implementar reglas y procesos para el control de versiones y el retiro de APIs.
- ### Auditar periódicamente el acceso a APIs de terceros y garantizar una protección óptima.

-----
# #10 Unsafe Consumption of APIs
Los desarrolladores tienden a confiar en los datos recibidos de APIs de terceros más que en la entrada de usuarios, por lo que tienden a adoptar estándares de seguridad más débiles. Para comprometer APIs, los atacantes se centran en servicios de terceros integrados en lugar de intentar comprometer directamente la API objetivo.

## **Como se acontece?**

Mediante el uso de APIs de terceros que generalmente son confiables, si se explotan estas apies de terceros pueden usarse para atacar APIs que dependen de estas.

## **Ejemplo**:
- ### El atacante inserta datos maliciosos en el sitio de validación de direcciones utilizado por el cliente. El atacante envía una solicitud al cliente para extraer específicamente datos explotados de un tercero. El cliente falla en no validar los datos y es explotado.
- ### El atacante compromete la API de terceros, lo que hace que responda con una redirección a un sitio malicioso. El client sigue ciegamente las direcciones sin validación y es explotado.
## **Riesgos**:
- ### Robo de datos.
- ### Intrusión al sistema. (Brecha de seguridad).
- ### Apropiación de cuentas.
## **Prevención**:
- ### Evaluar los controles de seguridad de la API de terceros.
- ### Validar los datos devueltos por API de terceros 
- ### Encriptar todas las comunicaciones entre APIs.
- ### Mantener una lista actualizada direcciones conocidas donde las APIs integradas pueden ser redirigidas.
