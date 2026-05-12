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

#### Power Chain




----

[^1]: **Serial Peripheral Interface** (*SPI*) es un protocolo asíncrono, full-duplex, con comunicación serial de cuatro cables. Es utilizado en cortas distancias y con una gran velocidad de transferencia de datos entre el microcontrolador (Master) y periféricos *ICs* (*Integrated Circuits*) como sensores, pantallas y tarjetas SD.
