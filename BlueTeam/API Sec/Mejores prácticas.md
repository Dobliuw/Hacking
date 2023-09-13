---------------------
-  Tags: #teoria #practica #blue #basico
---------------------
# Conclusión
### Como se puede ver en [[Los 3 pilares - (API Sec)]], es muy imporante hacer uso de **Governance**, es necesario tomarse el tiempo para definir las políticas, los estándares, los procesos, para asegurarse de que ningna API entre en funcionamiento sin pasar por el proceso adecuado y sin pasar todas las puertas de docuemntación, pruebas, seguridad y validación. Un gateway es excelente para hacer cumplir esto y asegurar se de que todas las API administren, imlemente y operen de manera consistente.
### Por otro lado, implementar un programa de **Testing** para qeu cada endpoint se apurebe en todos los vectores de ataque que exista. Buscará eejcutar todas als combinaciones de pruebase en cada objeto de datos, tipo de usuario, gfunción y método, y crear una cobertra completa. Obviamente esto requiere generar miles de escenarios de ataque para probar la respuesta "bajo presión" de la API en estos. La única manera de lograrlo es mediante la automatización y las pruebas continuas. Como bien sabemos es verdad que mayormente las APIs no cambian, es decir los endpoints suelen ser siempre iguales, pero no esta de más testear frecuentemente la respuesta y comportamiento de los mismos por posibles cambios en el código, infraestructura.
### Por último, **monitoring**, desarrollar un conjunto de métricas para seguir el progreso, cuántas vulnerabilidades se encuentra, con qué rapidez se mitigan, etc.

![[api_best_practices_1.png]]
![[api_best_practices_2.png]]
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