# Radio Control

Una **Radio Control**, también conocida como *Transmitter*, *Emisora*, *Radio*, *transmisora*, etc. es el "joystick" que se utiliza para enviar señales de radio al receptor (RX) del drone con el fin de poder pilotearlo de forma remota. Es el dispositivo físico que se sositene en las manos y desde el que se envían órdenes de vuelo.

Funcionamiento:

1. **Transmitter** (*Radio* / TX): Capta los movimientos que realizamos con los sticks / gimbals, botones y palancas para convertir esa información y envíarla a través de ondas de radio.
2. **Receiver** (RX): Dispositivo soldado al FC del drone que recibe esas señales emitidas previamente por la radio y las pasa a la *FC* (*Fligth Controller*) para que ajuste los motores mediante el ESC (*Electronic Speed Controller*).

Existen distintos tipos de radio (Mayormente ligados a un aspecto visual - funcional), donde a mayor tamaño mayor potencia / alcance, botones o accionables configurables, técnología, etc.

![[Pasted image 20260914154951.png]]  ![[Pasted image 20260914155014.png]] ![[Pasted image 20260914155118.png]]

-----
# Radio Features

A la hora de entender la necesidad que tenemos de cara a caracteristicas técnicas que tiene una radio, podemos hablar de *bandas*, *potencia*, *canales*, *alcance*, etc. Todo esto irá (Por lo general) directamente relacionado al tamaño, precio y calidad de la radio.
###### Frequencies & Bands

La radiofrecuencia (Visitar [[0. Radiofrequency Modulation]], [[1. Radiofrequency Demodulation]] y [[3. Radio Frequency Spectrum]]) es el medio fisíco por el que viaja la información. Las bandas más utilizadas en drones suele ser:

- **2.4GHz**: Es el estándar para el *control del  drone* (Radio). Ofrece un buen equilibrio entre alcance, ancho de banda y tamaño de antena. Es una banda *ISM* (Industrial, Scientific and Medical), de uso libre sin licencia en la mayoría de los países, lo que la hace muy popular pero también congestionada (WiFi, Bluettooth y otros dispositivos comparten el espectro).
- **5.8GHz**: Se usa sobre todo para la transmisión de video FPV. Tiene más ancho de banda pero *menor penetración* a tavés de obstáculos, ya que a mayor frecuencia, mayor atenuación por objetos. (Pero también mayor velocidad de transmisión - menor ms's / latencia).
- **900MHz**:  Usada por sistemas *long range*. A menor frecuencia, mejor penetración y difracción alrededor de obstáculos, lo que da un mayor alcance efectivo a costo de necesitar antenas má grandes.
- **433MHz**: Empleada en algunos sistemas de telemetría de long range, aunqeu su uso está mas restringido legalmente en muchos países.

###### Channels

Cuando hablamos de canales se pueden tender a referenciar dos cuestiones diferentes relacionadas al tópico FPV:

1. **Control Channels** (Functions): Cada acción controlable es un *canal lógico*, por ejemplo Throttle, Yaw, Pitch y Roll son los más básicos, pero existen otros. Una radio de "8 canales" puede hacer referencia a la transmisión de 8 valores independientes, sumando switches, diales, etc. cada canal transmite típicamente un valor númerico.

2. **RF Channels** (Frequency): Esta es la definición por excelencia a la cual se suele hacer referencia cuando se menciona la palabra "canales" de cara a la radio control de un drone. Como se puede ver en [[3. Radio Frequency Spectrum]], dentro de *una banda el espacio se divide en subcanales o frecuencias diferentes*. Por ejemplo, en 2.4GHz el sistema salta entre múltiples frecuencias. 

###### Modulation & Frequency Hope

Los sistemas modernos casi nunca usan una sola frecuencia fija. Emplean técnicas de espectro ensanchado:

- **FHSS** (*Frequency Hopping Spread Spectrum*): El transmisor y el receptor saltan de frecuencia decenas o cientos de veces por segundo siguiendo una secuencia pseudoaleatoria conocida por ambos. Esto da robustez frente a interferencias, ocupación de frecuencias y permite a muchos equipos convivir en la misma banda.
- **DSSS** (*Direct Sequence Spread Spectrum*): Distribuye la señal sobre un ancho de banda mayor mediante un código, mejorando la resistencia al ruido.

----
# Communication Protocols

Un **protocolo de comunicación** es un conjunto de reglas y normas estándar que permite a distintos dispositivos, computadores o sistemas de una red entenderse e intercambiar información de forma ordenada y sin errores.

En el caso del mundo de los drones, el **protocolo de enlace RF** (Entre tranmisor y receptor / RX-TX) existen distintos sistemas que compiten por el uso de los pilotos:

- **ExpressLRS** ([ELRS](https://github.com/expresslrs/expresslrs)) Protocolo OpenSource, muy popular con gran enlace y baja latencia. Pudiendo operar en `2.4GHz` o `900MHz`. 
- **TBS Crossfire**: Protocolo desarrollado por [BlackSheep](https://www.team-blacksheep.com/) nuevamente orientado a comunicación long-range (`900MHz`) y baja latencia `2.4GHz`.
- **FRSky ACCST** / **ACCESS**: Protocolos propietarios muy extendidos.

De cara a los **protocolos de transferencia de datos** de manera local (Entre receptor y FC):

- **PWM**: Un cable por canal. Antiguo y ocupa muchos pines.
- **PPM**: Varios canales multiplexados en un solo cable.
- **SBUS**: Digital, serie, hasta 16-18 canales por un cable. Señal invertida.
- **IBUS**: Protocolos digitales serie. *CRSF* es especialmente interesante porque ofrece baja latencia y telemetría bidireccional integrada.