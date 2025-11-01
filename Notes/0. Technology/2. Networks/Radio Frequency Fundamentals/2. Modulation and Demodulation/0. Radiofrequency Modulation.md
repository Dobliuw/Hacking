# Modulation 

Una onda portadora es una onda pura de frecuencia constante... por sí sola, no transporta mucha información con la que podamos relacionarnos (Como voz o datos). Por lo que, para *transmitir información* (Voz, música, datos, comandos, etc.), es necesario *superponer otra onda*. Este proceso de superposición de un *input signal* (*Señal de entrada*) sobre una *carrier wave* (*Onda portadora*) es denominado **modulación**. En otras palabras, la base de las **comunicaciones usando ondas electromagneticas**.

Cualquier estrategía que combine una señal de entrada con una onda portadora para codificar la voz u otra información últi se denomina **esquema de modulación**

Los esquemas de modulación pueden ser `análogicos` o `digitales`. Un **esquema de modulacón análogico** tiene una onda de entrada que varía continuamente como una onda sinusoidal. En el **esquema de modulación digital** es un poco más complitado. La voz se *muestra a cierta velocidad* y *luego se comprime* y *se convierte en un flujo de bits* (Una secuencia de  ceros y unos), que a su vez transforma en un tipo particular de onda que luego se superpone a la portadora.

Ahora... tal vez podrían preguntarse (Como yo al empezar a estudiar estos temas), algo como ¿Por qué utilizar ondas portadoras en la modulación? ¿Por qué no utilizar directamente la señal de entrada? Al fin y al cabo, contiene toda la información que nos interesa y solo ocupa unos pocos kHz y ancho de banda. ¿Entonces?

Bueno, las señales de entrada podrían transportarse (Sin una onda portadora) mediante ondas electromagnéticas de muy baja frecuencia. Sin embargo, el problema es que esto requeriría una amplificación considerable par transmitir esas frecuencias tan bajas. Las señales de entrada en sí mismas no tienen mucha potencia y necesitan una antena bastante grande para transmitir la información.

Para que la comunicación sea barata y cómoda y requiera menos potencia para transportar la mayor cantidad de información posible, se utilizan sistemas portadores con portadoras moduladas.

###### Input Signal

La **señal de entrada** (**Input Signal**) es, simplemente, la *información que queremos transmitir*. Esta señal no puede ser tranasmitida al aire directamente por dos principales motivos:

1. Es de *muy baja frecuencia*, no se propaga bien (Muy baja energía, muy poco penetración).
2. No podría *compartir espectro* con otras transmisiones: todas sonarían en el mismo rango y se mezclarían.

Por ejemplo, un micrófono convierte las *variaciones de presión del aire* (La voz) en una **señal eléctrica análogica**.
- Esta señal eléctrica es una onda de *muy baja frecuencia* (`20Hz`a `4kHz`).
- A veces se denomina *baseband signal* (Señal en *banda base*).

 La **input signal** muchas veces se ve representada como:  $V(t)$

----
###### Carrier Wave

La **onda portadora** (**Carrier Wave**) es generada por el *transmisor* como una *onda senoidal pura* (Sigue la función seno, suave y repetitiva / perfecta). A su vez el **transmisor** o **transmitter** suele ser un *oscilador electrónico* que produce una señal de corriente alterna con una forma de onda senoidal.

![[Pasted image 20250729204906.png]]

La **carrier wave** muchas veces se ve representada como:  $C(t) = A \times sin(2πf \times t)$

----
###### Modulator

El **modulador** (**Modulator**) es un *dispositivo*, *circuito* o *algoritmo matemático* que recibe la **input signal** como una *función de voltaje que varía en el tiempo* y  superpone esta señal con la **carrier wave** para la transmisión de esta señal entrante original (*Datos*) inálambricamente.

---

De cualquier manera, para entender esto en profundidad, es importante remitirnos a las **propiedades de las ondas** ([[1. Electromagnetics Waves Properties]]) entendiendo que para este caso, las propiedades relevantes de una onda son:

1. `Amplitude`: La altura de la onda medida desde el equilibrio. ([[1. Electromagnetics Waves Properties#Amplitude]]).
2. `Frequency`: Cantidad de ondas transmitidas en un ciclo. ([[1. Electromagnetics Waves Properties#Frequency (Hz)]]).
3. `Phase`: Desplazamiento en relación al tiempo. ([[1. Electromagnetics Waves Properties#Phase]]).


-----
# Analog Modulation

Los esquemas de **modulación análogica** es el proceso de *modificar una onda portadora continua* (Como una onda senoidal) alterando sus propiedades (Amplitud, Frecuencia, Fase) en proporción directa a una señal de entrada tambén análogica (Como la voz, la música, sensores, etc.). 

Este esquema de modulación trae consigo los tres primeros tipos de esta modulación:

- `Amplitude Modulation` (`AM`).
- `Frequency Modulation` (`FM`).
- `Phase Modulation` (`PM`).
### Amplitude Modulation (AM)

Existen *diferentes estrategias* de **modulación** para una onda portadora. Por ejemplo, un usuario puede *modificar el alto* de una onda (`Amplitude`). Si la altura de la *señal de entrada* (*Input Signal*) varía con el volumen de la voz y luego *se añade* a la *onda portadora* (*Carrier Wave*), la `amplitud`de esta última cambiará en función de la señal de entrada que se le haya suministrado. A esto lo denominamos `Amplitude Modulation`(`AM`).

![[Pasted image 20250729214812.png|900]]

### Frequency Modulation (FM)

Otra manera de **modular** una señal es modificando  le `frecuencia`, si esta señal de entrada se añade a la onda portadora pura, cambiará la frecuencia de la onda portadora. De este podo, los usuarios pueden utilizar los cambios de frecuencia para transmitir información de voz. Esto se denomina `Frequency Modulation` (`FM`).


![[Pasted image 20250729214724.png|900]]

### Phase Modulation

Esta manera de **modular** consiste en modificar los ángulos de la `fase` para con la señal portadora. Esta técnica de modulación es esencial en la mayoría de los sistemas de comunicación digital y ofrece un mejor rendimiento en términos de tolerancia al ruido y la calidad de la señal. Esto es posible gracias a la alteración de la fase de la portadora en relación con la amplitud; la modulación de fase *fascilita la transmisión de datos utiilzando presión* y otros tipos de canales de comunicación.

Este tipo de modulación se denomina `Phase Modulation` (`PM`).


![[Pasted image 20250729223938.png]]

# Digital Modulation

La **modulación digital** (**Digital Modulation**) consiste en codificar bits (`0` y `1`) en una señal portadora *modificando propiedades físicas* (Amplitud, Frecuencia, Fase) de forma *discreta* (En pasos, no continuamente como AM/FM).

Esta modulación es la base de todo lo que hoy en día conocemos, WiFi, BLE, Bluetooth, 4G, GPS, SDR Hacking, etc.

A diferencia de la *modulación análogica*, no hay una *mezcla de ondas*, si no, una **modificación  discreta** de la portadora por cada bit o símbolo. Es decir, se generan versiones "cuantizadas" de la portadora, y cada una representa cierta información binaria.

![[Pasted image 20250729225521.png]]

| Name   | Slang                                                      | Modulation in?          | Explanation                             |
| ------ | ---------------------------------------------------------- | ----------------------- | --------------------------------------- |
| `ASK`  | **A**mplitude **S**hift **K**eying                         | *Amplitude*             | `1` = Onda con amplitud, `0` = sin onda |
| `FSK`  | **F**requency **S**hift **K**eying                         | *Frequency*             | `1` = 2.4GHz, `0` = 2.3GHz (Example)    |
| `PSK`  | **P**hase **S**hift **K**eying                             | *Phase*                 | `1` = 180°, `0` = 0°                    |
| `QAM`  | **Q**uadrature **A**mplitude **M**odulation                | *Amplitude* + *Phae*    | Codifica múltiples bits por simbolo.    |
| `OFDM` | **O**rthogonal **F**requency **D**ivision **M**ultiplexing | *Multiples Frequnecies* | Divide datos en muchas portadoras.      |

Esto es importante porq toda la comunicación moderna usa esta modulación y es importante para en futuros artículos entender y poder enfrentarnos a la misma en momentos para:

- Interceptar (**Sniff**)
- Inyectar / Modificar (**Spoof**)
- Reproducir (**Replay**)



