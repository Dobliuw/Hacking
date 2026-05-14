# Introduction

Este proyecto nace con el fin de aprender un poco más sobre electrónica de la mano de la IA, la capacidad de Research y algunos compañeros de rubro como [Lup1n](https://www.youtube.com/@Lup1n_3).

En este punto la idea es realizar un **Signal Disrupter** o **Jammer**, con el fin de mezclar conceptos de electrónica y software development, con Hacking y técnicas ofensivas.

La idea no es tener el típico proyecto básico de un jammer, si no, tratar de independizarlo con baterías y flujos de control de carga y uso, así como amplificar la potencia de los módulos de tranmisión para tener una herramienta realmente potente que pudiese llegar a ser wireless. 

En el mejor de los casos, teniendo una correcta distribución de componentes para ensamblar en una carcasa impresa en 3D a medida. (Veremos)

---
# Components

A continuación se detallan los componentes seleccionados, su funcionalidad y motivo de selección. Este no es el primer prototipo, he ido viendo y consiguiendo distintos componentes para posteriormente darme cuenta que quizá deberían haber mejores alternativas.

#### Controller 

`NodeMCU ESP32 38-Pin USB-C` como *microcontrolador*. ¿Por que? Porque el mismo cuenta con dos buses SPI; se necesitan ambos: uno para la pantalla que quiero ponerle para animar (`ILI9341`) y otro para los dos módulos *RF* (`NRF24L01`), bus compartido, pines CS independientes.

Además, dispone de suficientes pines *GPIO* para botones, pines de control del amplificador que pondré y LEDs de estado. El módulo WiFi/BLE integrado es una ventaja adicional para futuras funciones.

> [!warning] Power Draw
> El módulo NodeMCU incorpora un regulador AMS1117 LDO, lo cual hace que al alimentar con 5V, se regule la tensión a 3.3V para el núcleo. El propio ESP32 consume:
> - WiFi TX Activo: `~240 mA` a `3.3V`.
> - Activo sin WiFi: `~80-100 mA`.
> - Light sleep: `~0.8 mA`.
> - Deep sleep: `~10µA`.
>   
>   Esto nos da un consumo de `~150 mA` de media para est aaplicación (WiFi desactivado y procesamiento activo).
> 
>   
>----
>   
>**AMS1117 LDO Problem**
>
>El LDO integrado reduce la tensión de forma lineal: la diferencia entre la entrada de 5V y la salida de 3.3V se disipa en forma de calor. A `150mA: (5V - 3.3V) x 0,15A = 0.255W` desperdiciados en forma de calor en el LDO. No supone un problema con esta corriente, pero conviene saberlo: el *NodeMCU* se calentará likgeramente bajo carga.

#### Screen

Las interfaces de pantalla paralelas (Como de 8 o 16 bits) requieren entre 8 y 16 líneas de datos, además de las líneas de control. La pantalla `TFT 2.4" 240x320 Spi SD LLI9341 5V`,  con [^1]*SPI* (*Serial Peripheral Interface*) necesita 4 cables (MOSI, SCK, CS y DC) más el reset. En un prototipo con GPIO limitado y complejidad de cableado, SPI es la solución más adecuada.

El SPI de hardware del ESP32 puede alimentar el ILI9341 con la rapidez suficiente para una interfaz de usuario de estado.

El módulo admite 5V en VCC porque cuenta con un regulador LDO de 3.3V integrado. El propio chip ILI9341 funciona a 3.3V. Es necesario comprobar las líneas lógicas SPI; la mayoría de las placas de expansión incluyen convertidores de nivel, por lo que la lógica de 3.3V del ESP32 es compatible.

> [!warning] Power Draw
> 
> - Pantalla + Iluminación al máximo brillo: `~80-120mA` a `5V`.
> - Pantalla + Iluminación tenue 50%: `~50-60mA`.
>
>Esto nos da un consumo de `~80mA`, la retroiluminación será la principal consumidora de corriente de la pantalla.

#### RF Chain

El modulo **NRF24L01** es un transceptor de 2.4GHz de un solo chip encargado de toco el conjunto de funciones de radio:

- Modulación (GFSK).
- Encapsulación de paquetes.
- CRC.
- Acuse de recibo automático.
- Lógica de retransmisión.

El *ESP32* se comunica a través de SPI con este modulo, limitandose a enviar y recibir bytes de atos, sin necesidad de gestionar manualmente la sincronización RF.

En mi caso, para mejorar la potencia no solo seleccione unos *amplificadores*, si no también, *dos modulos*, en si con el fin de tener mayor generación de ruido para el espectro en búsca de saturar. Pero también nos da la posibilidad de utilizar dos canales simultáneamente o emple uno como TX y otro como RX al mismo tiempo, sin la limitación de semidúplex.

> [!warning] Power & Antenna Cut
> La *potencia* máxima de transmisión del NRF24L01 es de `0dBm` (`1 mW`), lo cual es muy bajo (Por ajuste legal), esto es lo que me llevo a querer ir un paso más allá para construir algo real, ya que la mayoría de tutoriales o proyectos de jammers son técnicamente funcionales en cortas distancias, lo cual lo vuelve en escenarios reales poco realista. Para ampliar el alcance y penetración de obstáculos, se necesita *amplificación*.
> 
> Ahora bien, por otro lado... ¿Por que y cómo hacer un *corte en la antena* impresa en PCB del módulo? Bueno, el NRF24l01 tiene una *antena de traza de PCB impresa* directamente en la placa. Esta traza está adaptada a `50 Ω` a `2.4 GHz` por su geometría.
> 
> Para conectar un *amplificador*, es necesario *cortar la traza* en el punto de alimentación de la antena y soldar un contector *cable coaxia*:
> 
> ![[Pasted image 20260513163414.png]] 
> 
> Haciendo que el *Copper Wire* vaya al *RF Pad* por el cual saldría la señal y aislar el *GND* de la antena para soldar a este la *Copper Mesh*. A continuación se demuestra el proceso llevado a cabo:
> 
> ![[Pasted image 20260513224625.png|320]] ![[Pasted image 20260513224645.png|300]] ![[Pasted image 20260513224706.png|365]] ![[Pasted image 20260513224813.png|300]] 
> 
> En mi caso, una vez soldado el cable coaxial al modulo RF, tuve que desoldar el conector SMA y soldar el otro extremo del cable a la entrada *Radio*:
> 
> ![[Pasted image 20260513224824.png|300]]

Por otro lado, el modulo **MCP73871 USB 5V** llego como remplazo luego de haber comprado y seleccionado el **TP4056**, el cual es únicamente un *cargador lineal*: Es decir, cuando se conecta el USB, se carga la batería y la alimeanción del dispositivo se alimeanta de la batería en todo momento, por lo que si la batería está descargada, el sistema no funciona hasta que se haya cargado lo suficiente.

El **MCP73871** es un circuito integrado de gestión de la ruta de alimentación. Dispone de *tres modos* que funcionan simultáneamente: *cargar la batería* desde la entrada, *alimentar la carga directamente desde la entrada* y *completar la alimentación con la batería* si la carga supera la capacidad de la entrada.


Otro modulo importante son los **MT3608 Setp-Up Converters**, necesarios ya que los *amplificadores de RF* necesitan `5V`para funcionar a la potencia nominal. La batería seleccionada suminstra entre `3V` y `4.2V`. En este contexto, no podríamos alimentar dispositivos de `5V`con un voltaje menor y esperar que funcione correctamente. El modulo **MT3608** es un convertidor de conmutación elevador (*boost*), tomando una entrada de tensión baja y proporcionando una tensión regulada de salida más alta.

> [!info] How it works internally?
> El **MT3608** conmuta un MOSFET interno a alta frecuencia (`~1.2MHz`). Cuando se cierra el circuito, la corriente se acumula en un inductor, almacenando energía magnéticamente. Al abrirse, el inductor libera esa energía en forma de un pico de tensión, superior a la tensión de entrada. 
> 
> Un condesador suaviza la tensión de salida. El circuito integrado ajusta el ciclo de trabajo de forma continua para mantener la tensión de salida deseada, independientemente de las variaciones en la tensión de entrada.

Ahora, ¿Por que *dos* **MT3608**? Cada *amplificador RF* consume entre `500mA` y `600mA`durante las ráfagas de transmisión. Si ambos comparten un mismo convertidor, una ráfaga de transmisión en el amplificador n°1, provocaría una caída de tensión en el raíl compartido, el amplificado n°2 detecta esa caida y puede desaturarse, lo que provocaría una caída de la potencia de salida o inestabilidad.

> [!warning] Efficiency math to know
> Para suministrar `5 V`a `500 mA` (`2.5 W` de potencia de salida):
> - Potencia de entrada necesaria = `2.5 W` ÷ `0.87` (Eficiencia) = `2.87 W` con una batería de `3.7 V`:
> 	- Corriente de entrada `2.87 W` ÷ `3.7 V` = `0.78 A` cada **MT3608** consume unos `780 mA`de la batería para alimentar un amplificador a plena potencia de transmisión (*TX*).
 
#### Power Chain




----

[^1]: **Serial Peripheral Interface** (*SPI*) es un protocolo asíncrono, full-duplex, con comunicación serial de cuatro cables. Es utilizado en cortas distancias y con una gran velocidad de transferencia de datos entre el microcontrolador (Master) y periféricos *ICs* (*Integrated Circuits*) como sensores, pantallas y tarjetas SD.
