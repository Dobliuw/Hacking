---------------------
-  Tags: #teoria #practica #blue #basico
---------------------
# Conclusión
Como se puede ver en [[Los 3 pilares - (API Sec)]], es muy imporante hacer uso de **Governance**, es necesario tomarse el tiempo para definir las políticas, los estándares, los procesos, para asegurarse de que ningna API entre en funcionamiento sin pasar por el proceso adecuado y sin pasar todas las puertas de docuemntación, pruebas, seguridad y validación. Un gateway es excelente para hacer cumplir esto y asegurar se de que todas las API administren, imlemente y operen de manera consistente.
Por otro lado, implementar un programa de **Testing** para qeu cada endpoint se apurebe en todos los vectores de ataque que exista. Buscará eejcutar todas als combinaciones de pruebase en cada objeto de datos, tipo de usuario, gfunción y método, y crear una cobertra completa. Obviamente esto requiere generar miles de escenarios de ataque para probar la respuesta "bajo presión" de la API en estos. La única manera de lograrlo es mediante la automatización y las pruebas continuas. Como bien sabemos es verdad que mayormente las APIs no cambian, es decir los endpoints suelen ser siempre iguales, pero no esta de más testear frecuentemente la respuesta y comportamiento de los mismos por posibles cambios en el código, infraestructura.
Por último, **monitoring**, desarrollar un conjunto de métricas para seguir el progreso, cuántas vulnerabilidades se encuentra, con qué rapidez se mitigan, etc.

# Mejores prácticas

Teniendo en cuenta una vez más [[Los 3 pilares - (API Sec)]]....
- ### **Governance** (Establecer procesos, proceddimientos, póliticas, para que se cumplan con la seguridad).
- ### **Testing** (Evaluar y analizar la API en busca de vulnerabilidades, esto para garantizar una seguridad robusta y resistente).
- ### **Monitoring** (Supervisar y analizar el tráfico y comportamiento de la API, para identificar amenazas, anomalías o vulnerabilidades en tiempo real).

## Imponer la Governance de API y establecer un control central
- ### Utilizar un gateway o plataforma de mercado para administrar y supervisar todas las APIs.
- ### No permitir que ninguna API se implemente sin pasar por un proceso riguroso de aprobación que incluya la documentación pruebas y evaluación de seguridad.
## Crear un Programa integral de testing
- ### Realizar pruebas exhaustivas en cada endpoint de la API, abordando todos los tipos de ataques [[OWASP Top 10 API]] y otros.
- ### Evalúar cada objeto de datos, tipo de usuario y función en busca de vulnerabilidades lógicas.
- ### Aprovechar la automatización para lograr una cobertura de testing completa y repetible.
## Implementar pruebas automatizadas y continuas
- ### Tener en cuenta que aunque las APIs rara vez cambian, en si el código y la infraestructura suele hacerlo.
- ### Cada versión o lanzamiento debe someterse a pruebas funcinales y de seguridad. 
- ### Integrar las pruebas en el canal de desarrollo continuo (CI/CD) para garantizar la detección temprana de problemas.
## Desarrollar métricas de seguridad y evaluar el progreso
- ### Llevar un registro de todas las APIs que se gestionan, incluyendo las nuevas, existentes y retiradas.
- ### Mantener un registro de las vulnerabilidades identificadas, las pendientes de solución y las ya resueltas.
- ### Utilizar estas métricas para evaluar continuamente la seguridad e tus APIs y mejorar tus prácticas.
## Implementar la Autenticación y Autorización correcta:
- ### Utillizar estándares sólidos de autenticación, como OAuth 2.0, y asegurarse de que los usuarios y aplicaciones solo tengan acceso a las partes de la API que necesitan.
## Gestionar errores de manera segura:
- ### Evitar exponer información sensible en mensajes de error. En su lugar, proporcionar mensajes genéricos para los errores y registrar los detalles de error de manera segura en el servidor.
## Actualizar y parchear regularmente
- ### Es de vital importancia mantener la infraestructura y las bibliotecas utilizadas actualizadas. Aplicar parches de seguridad tan pronto como estén disponibles para evitar vulnerabilidades conocidas.
## Plan de respuesta de incidentes
- ### Preparar un plan de respuesta a incidentes qeu especifique cómo actuar en caso de una brecha de seguridad en la API. Practicar simulacros para asegurarse de que todos conozcan los procedimientos y para evaluar la capacidad de accionar.

# Que hacer y que no hacer
- ### No confiar en nada (Inputs/Networks).
- ### Validar **todos** los inputs (No solo los del usuario).
- ### No confundir ofuscación con seguridad (Mantener los elementos confidenciales fuera del código).
- ### No hardcodear keys/tokens.
- ### No revelar información importante sobre el uso en mensajes de errores.
- ### No tener características ocultas o no anunciadas.
- ### No filtrar datos en UI (Control en el nivel de App).
- ### No confundir autenticación con autorización.
- ### Hacer uso de Gateway para controlar el acceso y el tráfico.
- ### Tener documentación de la API.
- ### Esperar que los usuarios/ciberdelincuentes encuentren y usen endpoints no documentados.
- ### Realizar **testing** continuo (Simulación de ataques, test a configuraciones, fuzzing, inyecciones, autenticación, etc...).