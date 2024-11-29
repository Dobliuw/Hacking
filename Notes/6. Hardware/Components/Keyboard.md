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

#### Linux

Para lograr visualizar esto en un sistema operativo Linux podríamos llevar a cabo las siguientes instrucciones:

- Localizar dispositivos de entrada: 
```bash
ls -l  /dev/input/by-id/
```

En este punto, buscariamos el dispisitvo relacionado con nuestro teclado, este podría incluir `kbd`, `keyboard`, etc. Lo importante es visualizar a que *evento* apunta este **enlace simbolico**. 

- Hacer uso de `cat` para monitorear los eventos:
```bash
sudo cat /dev/input/{eventX}

# Replace "eventX" with the correct device
```

Estos eventos serán visualizados en formato *binario*.

- Hacer uso de `evtest` para mayor legibilidad:
```bash
sudo apt install evtest

sudo evtest /dev/input/{eventX}

# Replace "eventX" with the correct device
```

Como vimos en este artículo, los eventos del teclado son manejados en tiempo real por el sistema operativo y expuestos a trav´pes de `/dev/input/event*` en sistemas operativos Unix. Cada evento contiene información como:

- **Key Code**.
- **State** (Presionada o Liberada).

---
# Windows with C

En este ejemplo práctico intentaremos realizar un **hook**, el cual en el contexto de sistemas opeartivos, especialmente *Windows*, es un mecanismo que permite interceptar y modificar el flujo de eventos del sistema o de una aplicación. En término más simples, un hook es una herramienta que podemos utilizar para "engancharnos" al sistema operativo y observar o alterar eventos como pulsaciones de teclado, clicks de mouse, creación de ventanas, entre otros.

La idea será utilizar `WinAPI` (La API de Windows) para:

- Interceptar eventos de teclado en el sistema operativo.
- Mostrar las teclas persionadas en la consola.
- Funcionar como un programa que escucha en tiempo real.

El código se estructurara en *la definición del hook* del teclado, la *configración del lopp* para capturar eventos y la *liberación del hook* para cuando el programa termine.

Para este código utilizaremos las librerías `windows.h` y `stdio.h`, las cuales:

- `stdio.h`: Se usa para imprimir información el la consola (La utilizaremos para funciones típicas como *printf*).
- `windows.h`: Contiene las funciones y estructuras necesarias para interactuar con el sistema operativo Windows, como funciones que utilzaremos *SetWindowsHookEx* y *CallNextHookEx*. 

Una vez importadas las librerías necesarias, **definieremos la función del Hook**:

```C
LRESULT CALLBACK LowLevelKeyboardProc(int nCode, WPARAM wParam, LPARAM, lParam){
    if(nCode == HC_ACTION){
        KBDLLHOOKSTRUCT *kbdStruct = (KBDLLHOOKSTRUCT *)lParam;

        if(wParam == WM_KEYDOWN){
            printf("Key pressed: %d\n", kbdStruct->vkCode);
        };
    };
};
```

- `LowLevelKeyboardProc` será la función qeu se ejecutará cada vez que se presione o suelte una tecla.
	- `int nCode`:
		- Indica si el evento debe ser procesado o ignorado.
		- `HC_ACTION` singigica que hay un evento de teclado que procesar.
	- `WPARAM wParam`:
		- Especifica el tipo de evento, Los valores importantes son:
			- `WM_KEYDOWN`: Una tecla fue presionada.
			- `WM_KEYUP`: Una tecla fue libereda.
	- `LPARAM lParam`:
		- Apunta a una estructura `KBDLLHOOKSTRUCT`, que contiene información sobre la tecla presionada (Por ejemplo, su código virtual)

 Posteriormente a haber *procesado el evento de teclado* e *impreso la tecla*, deberemos pasar el control al *siguiente hook*. La línea que se encargara de esto será:

```C
...........{
	..............
	return CallNextHookEx(NULL, nCode, wParam, lParam);
};
```

- `CallNextHookEx`:
	- Llama al siguiente hook en la cadena de hooks.
	- Es importante incluir esto para no bloquear otroos porgramas que necesiten procesar los eventos del teclado.

Luego, deberemos *configurar el Hook* en la función `main` de nuestro script:

```C
int main(){
    HHOOK keyboardHook = SetWindowsHookEx(WH_KEYBOARD_LL, LowLevelKeyboardProc, NULL, 0);
    ........
};
```

- `SetWindowsHookEx`:
	- Instalar el hook de teclado a nivel de sistema.
	- Los *parámetros* son:
		- `WH_KEYBOARD_LL`: Específica que el hook será de nivel bajo para el teclado.
		- `LowLevelKeyboardProc`: Nombre de la función que preocsará los eventos de teclado que declaramos al principio del código.
		- **NULL**: Se usa el módulo actual.
		- **0**: El hook se aplica a todos los hilos del sistema.
- `HOOK keyboardHook`:
	- Es un identificador que representa el hook instalado.

Posteriormente, verificariamos si el Hook se isntaló correctamente:

```C
int main(){
	........
	 if (keyboardHook == NULL){
        printf("Failed to install keyboard hook.\n");
        return 1;
    }
    ........
};
```

Casi por último *Capturariamos Mnesajes del Sistema*:

```C

	........
	MSG msg;
    while (GetMessage(&msg, NULL, 0, 0)) {
        TranslateMessage(&msg);
        DispatchMessage(&msg);
    }
    ........
};
```

- `MSG msg`: Estructura que almacena mensajes del sistema opeartivo.
- `GetMessage`:
	- Escucha los mensajes del sistema y los para al programa.
	- Este loop permite que el program funcione continuamente, esperando eventos de teclado.
- `TransLateMessage` y `DispatchMessage`:
	- Procesan los mensajes capturados para que el sistema opeartivos puede manejarlos correctamente.}

Ahora sí, por último simplemente quedaría liberar el Hook al salir del programa:

```C
int main {
	.....
	UnhookWindowsHookEx(keyboardHook);
	return 0;
}
```

- `UnhookWindowsHookEx`:
	- Libera el hook para evitar que quede activo después de que el programa termine.
	- Esto es importante para liberar recursos en el sistema.

Finalmente nuestro código quedaría de la siguiente manera:

```C
#include <windows.h>
// We need interact with WinAPI, the windows.h module we help us
#include <stdio.h>

LRESULT CALLBACK LowLevelKeyboardProc(int nCode, WPARAM wParam, LPARAM lParam){
    if(nCode == HC_ACTION){
        KBDLLHOOKSTRUCT *kbdStruct = (KBDLLHOOKSTRUCT *)lParam;

        if(wParam == WM_KEYDOWN){
            printf("Key pressed: %d\n", kbdStruct->vkCode);
        };
    };
    return CallNextHookEx(NULL, nCode, wParam, lParam);
};

int main(){
    HHOOK keyboardHook = SetWindowsHookEx(WH_KEYBOARD_LL, LowLevelKeyboardProc, NULL, 0);

    if (keyboardHook == NULL){
        printf("Failed to install keyboard hook.\n");
        return 1;
    }

    printf("Key logger running...\n");

    MSG msg;
    while (GetMessage(&msg, NULL, 0, 0)){
        TranslateMessage(&msg);
        DispatchMEssage(&msg);
    }

    UnhookWindowsHookEx(keyboardHook);
    return 0;
};
```