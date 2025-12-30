# Key parts

Un dron no es una sola cosa, es la integración de *6 subsistemas críticos*.

### Structure (Frame)

Es la **estructura física** que ensambla todos los demás componentes y partes del dron. Su principal función es:

- Soportar peso.
- Absorver vibraciones.
- Resistir impactos.
- Mantener alineación de motores.

En **FPV** se suele utilizar:

- Fibra de carbono (Para mayor rigidez y menor peso).
- Diseño modular (Brazos reemplazables).

Y esto define el tamaño del dron (5", 7", 10").

![[Pasted image 20251229155419.png|315]]  ![[Pasted image 20251229155429.png | 400]] ![[Pasted image 20251229155449.png|418]]
### Propulsion (Motors + Propellers)

El **sistema de propulsión** es el sistema que *genera empuje* y se compone de **motores brushless** (Sin escobillas) y **hélices** (Propellers). El dron no se eleva empujando hacia arriba, se eleva empujando aire hacia abajo, el empuje depende de:

- Tamaño de hélice.
- Pitch.
- RPM (Revoluciones por minuto).
- Eficiencia del motor

En **FPV**:

- Motores grandes + hélices grandes = mayor eficiencia.
- KV bajo (Velocidad del motor) = menos RPM = menos consumo.

> [!info] KV 
> $$
> KV = \frac{RPM}{Volt}
> $$

> [!info] Pitch
> Distancia teórica que avanzaría la hélice en un medio sólido por cada revolución completa y se mide en pulgadas. Se mide en pulgadas:
> 
>-  hélice 7x4
>	- 7" = Diámetro.
>	- 4" = Pitch.
>
>NO es el ángulo, es el movimiento de inclinación hacia arriba o hacia abajo de la nariz, controlado mediante el ajuste de la velocidad de los motores para mover el dron hacia adelante (Nariz hacia abajo) o hacia atrás (Nariz hacia arriba).

![[Pasted image 20251229155753.png|490]] ![[Pasted image 20251229155828.png|550]]

### Power Control

Es **control de potencia** es el intermediario entre baterias y motores. Su función es recibir órdenes del *flight controller*, ajustar cuánta energía llega a cada motor y controlar la velocidad y frenado.

En **FPV**:

- Se suele buscar un control de potencia ultra rápido (Miles de ajustes por segundo).
- Puede ser:
	- 4 ESC individuales.
	- 4-in-1 ESC (Lo más común).

![[Pasted image 20251229160151.png|400]] ![[Pasted image 20251229160221.png|605]]

### Flight Controller (FC)

El **controlador de vuelo**, como la palabra lo dice es el controlador central, donde se producen la mayor cantidad de operaciones, cálculos y ejecución de software. Suele contener:

- Microcontrolador.
- Giroscopio (IMU).
- Acelerómetro.
- Barómetro (A veces).
- Brújula (A  veces).

Dentro de las actividades que realiza:

- Lee sensores cientos de veces por segundo.
- Calcula orientación y rotación.
- Ejecuta algoritmos de control (PID).
- Decide cuánto acelerara cada motor.

### Energy (Battery + Distribution)

Como sabemos, la **energía** ([[2. Key Concepts#Power]]) es la fuente que le permite a los otros sistemas realizar sus operaciones durante un determinado tiempo (Según `mAh`). Es la fuente de energía que determina el tiempo de vuelvo ante todo... y existen dos tipos:

 - LiPo: Potencia instantánea.
 - Li-ion: Eficiencia energética.

En **FPV**:

- Conectada directamente al ESC (Electronic Speed Controller).
- Alimenta motores, fligth control, sistema FPV y receptor.

![[Pasted image 20251229161217.png|400]]  ![[Pasted image 20251229161253.png|360]]  ![[Pasted image 20251229161231.png|330]]

### Radio Link (Remote Control)

El **enlace de radio** es la manera que tenemos de controlar los motores de manera remota a través de dos componentes principales, propios de las *radio frecuencias* (Visitar la sección [[1. Electromagnetics Waves Properties#The first electromagnetic Wave]]), que son:

- Radio (En forma de control en las manos del operador).
- Receptor (En el dron).

En **FPV**:

- Muy baja latencia.
- Muy alta confiabilidad.
- ELRS es el estándar actual.

> [!info] ELRS 
> **ELRS** (**ExpressLRS**) es un *radio control system* para drones y modelos RC de *código abierto*, *long-range* y *low-latency*, principalmente conocido por ser el estándar actual debido a su alto rendimiento y fiabilidad.

![[Pasted image 20251229182639.png|406]] ![[Pasted image 20251229182652.png|450]] ![[Pasted image 20251229182723.png|410]]

### Vision (FPV System - Video)

El **sistema FPV** en un dron es una tecnología que transmite video en tiempo real desde la cámara del dron a unas gafas o pantalla del piloto, permitiéndole controlar como si estuviera "dentro" de ella. Los componentes suelen ser:

- Cámara FPV.
- Transmisor de video (VTX).
- Googles.

![[Pasted image 20251229183036.png|600]]