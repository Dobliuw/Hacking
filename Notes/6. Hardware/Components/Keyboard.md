# Keyboard Low-Level Funcionality

¿Alguna vez se han preguntado que es lo que ocurre a bajo nivel cuando presionamos una tecla del teclado? Si es así estan en el artículo correcto... en este artículo describiremos el proceso que ocurre a la hora de presionar una tecla en el teclado.

El proceso de presionar una tecla determinada y verla reflejada en un software es una buena demostración de lo que al fin y al cabo es un sistema informático: un conjunto de dispositivos que introducen, procesan, emiten y almacenan datos.

Es un buen kick off para visualizar como el hardware de una computadora se comunica con el software, y aunque pueda parecer un proceso secillo, involucra un complejo sistema de hardware, software y comunicación a bajo nivel.

---
# 1. Electrical Signal Generation

Cuando presionamos una tecla ocurren dos cosas:
#### Key Matrix

El teclado tiene un circuito llamado **matriz de teclas**, donde cada tecla corresponde a una intersección entre *filas* y *columnas*. Al presionar una tecla, se cierra un circuito eléctrico en esa intersección, lo que genera una señal eléctrica.
#### Microcontroler Detection

Una vez generada esta *señal eléctrica* por la *matriz de teclas*, el **microcontrolador del teclado** detecta qué fila y columna están conectadas y genera un **scan code** específico. (Es decir, un número único que representa una tecla). Por ejemplo, si presionamos la tecla `A`, el scan code podría ser `0x1C`.

Este **Scan Code** será el dato fundamental que se transmitirá al sistema para ser interpretado y procesado.

----
# 2. Scan Code Transmission

Una vez que tenemos el determinado *scan code* la forma en que el teclado comunica los datos al sistema depende del tipo de conexión que este tenga...
#### Transmission Protocol (PS/2 vs USB)

- *PS/2 Conecctions* (Sistemas Antiguos):
	- Los **scan codes** se envía como datos seriales directamente al *controlador de teclado Intel 8042* en la placa madre.
	- El controlador detecta el evento y genera la interrupción correspondiente.

- *USB Connection*:
	- Aca es donde entra en juego el **protocolo HID** (**Human Interface Device**):
		- El teclado organiza los *Scan Codes* en *HID Reports*.
		- Estos reportes son estructuras de datos compactas que conteiene información sobre el estado del teclado, como qué teclas están presionadas o liberadas.
		- El teclado transmite los reportes al sistema operativo a través del bus USB.

**NOTA**: *HID* es principalmente un **protocolo**, pero también el término se usa coloquialmente para referirise al controlador (*Driver*) que implementa ese protocolo en un sistema operativo.

- **HID Protocol**:
	- HID es un protocolo definido por la especificación USB para estandarizar cómo los dipositivos de entrada (Teclados, Mouse, etc.) comunican datos con un sistema operativo.
	- Este protocolo define cosas como los *formatos* de los *paquetes* de datos enviados desde el dispositivo y cómo se negocian los parámetros de comuniacción entre el dispositivo y el sistema.
- **HID Like Driver**:
	- En sistemas operativos modernos, el término *HID* también se usa para referirse a la *capa de software* (*Driver*) que implementa el protocolo HID.
	- El Driver HID actúa como intermediario entre el dispositivo físico y el sistema operativo.

#### Keyboard Controler in Mother Board

El **controlador del teclado** es un componente de hardware *en la placa madre* que actúa como intermediario entre el teclado y el sistema operativo. Este hardware *recibe* y *gestiona* los **scan codes** enviados por el teclado así como a su vez envía una señal al procesador mediante una *interrupción de hardware* para notificar que hay datos listos para ser procesados.

En sistemas antiguos (Como los basados en arquitectura x86), el controaldor de teclado más común era el *controlador Intel 8042*. Aunque en hardware moderno este controlador ha sido reemplazado o emulado, su funcionalidad básica sigue siendo lo relevante.

En *hardware moderno*, los sistemas *x64* con teclados **USB**, los controladores HID (**Human Interface Device**) y el **chipset USB** realizan funciones equivalentes, pero el principio de interrupción sigue siendo el mismo.

---
# 3. CPU and OS Processing

Una vez que el teclado ha generado y transmitido el *scan code* al sistema, el trabajo pasa al **Procesador** (**CPU**) y al **Sistema Operativo**, que juntos interpretan este código para convertirlo en un carácter o acción que las aplicaciones puedan usar. Este proceso consta de varias etapas:
#### Interruptions and IDT

En sistemas x86 y x64, el controlador del teclado genera la interrupción **IRQ 1** (**Interrupt Request**). Esta interrupción se refiere a una línea de hardware específica en la arquitectura de la placa madre que envía una señal al procesador y está asignada al teclado por convención histórica.

Aunque el teclado aún genera señales equivalentes a *IRQ 1*, los sistemas modernos abstraen este proceso:

1. *Emulation and Controlers*:
	- En sistemas modernos con teclados USB, los controladores HID y el firmware (Como UEFI o BIOS) emulan este comportamiento.
	- Cuando presionamos una tecla, el controlador HID genera un evneto que el sistema operativo traduce como si fuera un interrupción IRQ 1.
2. *IDT* y *Interruption Vectors*:
	- En arquitecturas x64, las interrupciones de hardware están mapeadas en la **IDT** (**Interruptor Descriptor Table**), una estructura que mapea cada interrupción a un manejador de interrupciones específico (**ISR** - **Interrupt Service Routine**).
	- IRQ 1 típicamente corresponde a un vector de interrupción definido por esta IDT.
3. *Real and Protected Mode*:
	- En **Real Mode** (Usado por sistemas antiguos), la interrupción IRQ 1 estaba directamente asignada a una dirección de memoria fija.
	- En **Protected Mode** o **Large Mode** (x64), el sistema operativo abstrae y gestiona esta interrupción a través de drivers y capas de software.

#### IDT Calling

En sistemas modernos (x64), las interrupciones están gestionadas por la **Interrupt Descriptor table** (**IDT**), una tabla que *mapea cada IRQ a una dirección de memoria* donde se encuentra el ISR correspondiente.

En este caso, la entrada en la IDT para *IRQ 1* apunta al **Keyboard Controller**, una función específica dentro del sistema operativo.

#### Interrupt Service Routine (ISR)

La **Interrupt Service Routing** (**ISR**) del teclado es ejecutada y contará con las siguientes responsabilidades:

1. **Leer** el *scan code* almacenado en el buffer del controlador del teclado (Generalmente a través de un puerto de *E/S*, como el puerto `0x60`en sistemas clásicos).
2. **Almacenar** este *scan code* en un buffer de entrada más accesible para el sistema operativo.

En este momento, el ISR no realiza traducciones, su tarea principal es asegurar que el scan code esté disponible para el sistema operativo.
#### Interruption Ending

Una vez procesado el Scan Code, la ISR envía una señal de fin de interrupción (**EOI** - **End Of Interruption**) al controlador programable de interrupciones (**PIC**/**APIC**), permitiendo que la CPU vuelva a su tarea original

---
# 4. Scan Code Translation by the OS

El **Sistema Operativo** ahora es capaz de obtener el *scan code* del *Buffer de entrada* y lo procesa en varias capas:
#### Mapping Scan Code to Key Code

El sistema operativo consulta un **keymap** (Mapa de teclas), una tabla que asocia cada scan code con una tecla lógica. Por ejemplo para el *scan code* `0x1C` se asocia con la tecla `a`. 

Este paso depende del diseño del teclado (Layout). Un teclado QERTY y un teclado AZERTY tendrán keympas diferentes.
#### Keys Modifiers

Si se presionan teclas modificadoras como la tecla `Shift`, `Alt` o `Ctrl`, el sistema operativoajusta el resultado del mapeo. Por ejemplo con la tecla `Shift` activa, el scan code `0x1C` podría traducirse a `A` en lugar de `a`.

---
# 5. Generating Input Events 

El resultado del mapeo se transforma en **Eventos de Entrada** / **Input Events** que pueden ser manejados por las aplicaciones.

En sistemas operativos modernos, estos eventos se representan como e structuras o mensajes específicos:

- En *Windows*, se generan mensajes como `WM_KEYDOWN` o `WM_KEYUP`, que contienen información sobre la tecla presionada.
- En *Linux*, se generan eventos en `/dev/input`, que pueden leerse con herramientas o APIs específicas como `libevdev` o `xinput`.

----
# 6. Sending Input Events to Applications

El sistema operativo coloca estos eventos en una **cola de entrada** *asociada a la ventana o preceso* que tiene el foco actualmente. Esto asegura que:

1. Solo la aplicación activa reciba los eventos, por ejemplo, si tenemos un editor de texto abierto, este recibirá el evento `KEY_a` y mostrará la letra `a` en pantalla.
2. Compatibilidad Multidispositivo, por ejemplo si varios teclados están conectados, los eventos pueden combinarse en la misma cola, permitiendo que múltiples dispositivos trabajen simultáneamente.

----
# Windows vs Linux

En *Windows*: 
- **Input System**: 
	- Los eventos se pasan a través de un sistema de mensajes de WIndows (*Message Queue*).
	- Cada ventada recibe mensajes como `WM_CHAR`, `WM_KEYDOWN` o `WM_KEYUP`, que indican qué tecla se presionó.

En *Linux*:
- **Direct Input Devices**:
	- Los eventso se manejan directamente desde dispositivos en `/dev/input`.
	- Aplicaciones pueden usar APIs de más alto nivel, com `Xlib` (*X11*), `Wayland` o `SDL`, para manejar entradas.

----



# Trying to Watch this

{Aca vendrían 2 ejemplos. Uno en linux y Windows con Wireshark}
Y otro con C en Windows
