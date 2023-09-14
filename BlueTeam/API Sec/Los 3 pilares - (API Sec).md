---------------------
-  Tags: #teoria #practica #blue #basico
---------------------
# Governance
### La "**gobernanza**" (**Governance**) se refiere a la gestión y control de las APIs para garantizar que cumplan con los requisitos de seguridad y políticas establecidas por una organización. Esto implcica establecer procesos, políticas y procedimientos que ayuden a administrar y supervisar de manera efectiva todas las actividades relacionadas con las APIS.

### Existen dos componentes para llevara cabo la **governance**. Por un lado la **conciencia** (**Awareness**) y por otro los **procesos y la política**.

![[governance_benefits_apisec.png]]
### Los beneficios de **Governance** consisten en establecer chorencia. Se trata de coherencia en cómo se desarrollan lasAPi, cómo se implementa, cómo se prueban, etc. Establecer expectativas para el equipo de ingeniería, ¿Qué se re quiere?, ¿Cuáles son esos requisitos de documentación y políticas de autenticación, control de versiones?, etc.

# Conocer las APIs

## **Obtener API de inventario completo**
- ### Objetivo, Dueño, Documentación.
### **Estandarizar y hacer cumplir el proceso de implementación de APIs
- ### La existencia de APIs 'shadow/rogue' son señales de una **governance** débil.
- ### Las API solo se implementan de forma aprobada y con la validación adecuada.
- ### Hacer cumplir la **Governance** en Gateway y Marketplaces.
### **Documentación de la API mandatoria**
- ### Asegúrarse de que las API sean coherentes y reutilizables.
- ### Defini requisitos de documentación.
### **Crear estándares de desarrollo de APIs**
- ### Guías de estilo, requisitos de autenticación, control de versiones, seguimiento de PII. 

# Conocer los riesgos

### **Identificar**: APIs, datos, paths de acceso (Amenzas potenciales).
### **Evaluar**: Vulnerabilidades, fallas lógicas, control de acceso, riesgos de terceras partes.
### **Probabilidad**: Examinar la probabilidad de un ataque.
### **Impacto**: Entender los daños, las perdidas y consecuencias de un potencial ataque.
### **Mitigación**: Desarrollar un plan para abordar el riesgo.

# Documentación: OpenAPI Specification (Swagger)
### **Swagger**, conocida como **OpenAPI Specification** es una herramienta y una especificación qeu se utiliza en el contexto de las APIs para describir, documentar y definir el comportamiento de una API de manera uniforme y estandarizada.
### Esto es super importante en el pilar de **Governance** ya que nos brinda múltiples ventajas de cara a la seguridad.

- ### No opcionales.
- ### Estándar de la industria para API REST.
- ### Machine-readable (YAML, JSON).
- ### Ayuda al desarrollo e integración de terceros.
- ### Ayuda al **testing**.
- ### Generadas de manera manual o auto generadas.
- ### Controla lo público y lo privado.
- ### Retirar documentación vieja (Puede ser un gran vector de amenazas).
- ### Definir las capacidades de la API (Titulo, descripción, version, Base-URL, endpoints, paths, request - response payloads, requerimientos de autenticación, parametros, tipos de datos, métodos).

# Guías de diseño: Promover la **Governance** y la consistencia.

- ### **Autenticación**: Tipo (Token, Basica, certificada), como implementarla.
- ### **Autorización**: Quien tiene acceso a que, donde se aplica.
- ### **Convención de nombres**: URIs como sustantivos, Metodos como verbos, plurulización, jerarquía, caso, lenguaje, sin abreviaciones/jerga.
- ### **Códigos de error**: Códigos de estado, IDs de referencia, mensajes legibles para humanos sobre el error (Sin especificaciones que puedan generar un vector a posibles amenzas).
- ### **Versionado**: Cuando actualizar, cuando no, tipos de versiones.
- ### **Únidades, Formatos y Standars**: Formatos date/time, timezones, etc.
### Ejemplo de Guía de diseño:

![[desing_guide_example.png]]

-----
# Testing
### El **testing** es la seguridad de las APIs se refiere a la práctica de evaluar y analizar una API específica en busca de vulnerabilidades, debilidades de seguridad y psoibles probelmas que puedan ser explotados por atacntes maliciosos. Estas pruebas se realizan para garantizar que la API sea robusta y resistente a ataques y cumpla con los estándares de seguridad establecidos. 

### Este pilar es fundamental para la seguridad de las APIs, por lo que es importante saber como realizar el [[Abuso de APIs]].

![[api_testing.png]]
# Categorias de **testing** 
## **Seguridad de la API** 
- ### Endpoints insegurods.
- ### Explotación en la autenticación.
- ### Enumeración (IDs, etc).
- ### Ataques DOS, limitación de la velocidad del tráfico.
- ### TLS (Transport Layer Security) faltante, problemas del SSL (Secure Sockets Layer).
- ### Fuzzing, validación de inputs.
- ### [[SSRF - (Server-Side Request Forgery)]].
- ### Propiedades del servidor leakeadas (Fuga de información).
## Seguridad de los DATOS
- ### Control de acceso.
- ### Exposición exesiva de datos.
- ### Exposición de datos sensibles.
- ### Datos personales, de salud o de bacos.
- ### Exposición de directorios o archivos.
- ### Cifrado en proceso.
- ### Exfiltración de datos.
## Logica de negocio
- ### Acceso a cuentas ajenas.
- ### Abuso de funcionalidades de la API.
- ### Control de acceso basado en roles.
- ### Pentesting.

-----
# Monitoring
### El **Monitoring** en la seguridad de las APIs se refiere al proceso de supervisar y analizar continuamente el tráfico y el comportamiento de una APi con el fin de identificar posbiles amenazas, anomalías y vulnerabilidades de seguridad en tiempo real o de manera proactiva. La monitorización  de seguridad de las APIs es esencial para detectar y responder a incidentes de seugirdad de manera oportuna y garantizar que la APi funcione de manera segura y eficiente. 

![[monitoring.png]]
### Esta fase, este pilar se relaciona a entender cómo se desempeñan y operan las APIs en producción. Una de las partes, **Runtime Protection** (**Protección en tiempos de ejecución**) hace referencia a protecciones activas en la API, esto incluye la aplicación de políticas, la exigencia de autenticación de los usuarios para acceder a los endpoints y el filtrado de tráfico. Este tipo de filtrado, por región, por IP, etc. puede ser una protección en tiempo real que podamos implementar.
### Por otro lado, **Threat Detection** (**Detección de amenzas**) refiere a ¿Como analizamos el tráfico apara buscar cosas como transacciones fraudulentas, tráfico fraudulento y ataques distrubuidos provenientes de muchas fuentes diferentes que apunta a recursos similares? ¿Se desea recibir alertas sobre esto y asegurarse de que se está controlando adecuadamente?. A su vez habilitar la respuesta a inicidentes, es decir, caputar el tráfico, registrar todo, colocarlo en un recursos para posteriormente volver sobre los pasos para comprender qué sucedió, que se intento realizar, etc.
### Por último, sin duda será necesario **Control Validation** (**Validar los controles**), para asegurar que todos los controles que se han implementado en el gateway, firewalls y en la aplicación funcionan según lo establecido y esperado. 

![[api_discovery.png]]
### De igual manera, es importante tener en cuenta que existen múltiples limitaciones sobre la **monitorización**, por lo que hay que tener especial cuidado en esta fase ya que podría incluso generar latencia en los servidores.

![[limitations_of_monitoring.png]]