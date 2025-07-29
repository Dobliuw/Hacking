# The OSI Model / El modelo OSI

El **Modelo OSI** es un *modelo teórico de referencia* que describe cómo los sistemas de red deberían comunicarse entre sí. Este está compuesto por *siete* (*7*) *capas* que permiten la estandarización de funciones de red específicas

| Layer | Layer Name       | Description                                                                                                                                                                                                                      |
| ----- | ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `7`   | **Application**  | Define protocolos para aplicaciones específicas utilizados para comunicaciones proceso a proceso (Ejemplo HTTP, FTP, etc.)                                                                                                       |
| `6`   | **Presentation** | Proporciona una representación c omún de los datos transferidos entre los servicios de capa de aplicación, traduciendo y conviertiendo los datos.                                                                                |
| `5`   | **Session**      | Esta capa proporciona servicios a la capa N° 6 para organizar el díalogo y administrar el intercambio de datos.                                                                                                                  |
| `4`   | **Transport**    | Define servicios para segmentar, transferir y volver a montar los datos para las comunicaciones individuales.                                                                                                                    |
| `3`   | **Network**      | Se encarga de fragmentar, transferir y volver a montar los datos enviados a través de la red, así como establecer el mejor camino definiendo el direccionamiento lógico.                                                         |
| `2`   | **Data Link**    | Los protocolos de la capa de enlace de datos describen métodoos para intercambiar datos, tramas entre dispositivos a través de un medio.                                                                                         |
| `1`   | **Physical**     | Los protocolos de capa física describen componentes emcánicos, electricos, funcionales y de procedimienots para activar, mantener y desactivar conexiones físicas para una trasmisión de bits hacia y desde una red dispositivo. |

![[OSI_TCP_IP_LAYERS 1.png]]

Para dejar un poco más claro, las capas de *2* a *4* están orientadas al transporte y desde las capas *5* a *7* están orientadas a la aplicación. En cada capa se realizan tareas definidas con precisión y se describen con precisión las interfaces con las capas vecinas. cada capa ofrece servicios para su uso en la capa directamente encima de ella. Para que estos servicios estén disponibles, la capa utiliza los servicios de la capa inferior y realiza las tareas de su capa.

Si dos sistemas se comunican, las siete capas del modelo OSI se ejecuta al menos dos veces, ya que tanto el emisor como el receptor deben tener en cuenta el modelo de capas. Por lo tanto, se debe realizar una gran cantidad de tareas diferentes en las capas individuales para garantizar la seguridad, confiabilidad y rendimiento de la comunicación.

Cuando una *aplicación* **envía un paquete** a otro sistema, el sistema trabaja con las capas que se muestran arriba *desde la capa 7 hasta la capa 1*, y el sistema *receptor* **descomprime el paquete** recibido *desde la capa 1 hasta la capa 7*. Podríamos entender esto viendo el ejemplo visual de [[osimodel_example.excalidraw]] donde podemos apreciar este flujo de datos.

También podemos ver [explicaciones del modelo OSI](https://www.youtube.com/watch?v=CnNRdJgeMo8) para entender aún mejor esto.