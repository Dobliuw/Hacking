# Analogic vs Digital

En FPV, el sistem ade video es un enlace de comunicaciones RF en tiempo real, no un "streaming" como el de consumo. Por lo que en pilotos profesionales se suele demandar la baja latencia, continua y predecible bajo  conficiones RF adversas.

![[Pasted image 20251229211310.png]]

| Parameter             | Analogic          | Digital              |
| --------------------- | ----------------- | -------------------- |
| Latencia              | Muy Baja (5-15ms) | Baja-Media (20-45ms) |
| Jitter                | Casi nulo         | Presente             |
| Degradación           | Gradual           | Brusca               |
| Calidad Imagen        | Baja              | Alta                 |
| Consumo               | Bajo              | Mayor                |
| Comportamiento límite | Volable           | Corte                |
| Complejidad           | Baja              | Alta                 |

###### Analog Video

El **video análogico FPV** funciona por modulación analógica directa de una señal de video compuesto (CVBS) sobre una portadora RF (Típicamente 5.8GHz, 2.4GHz o 1.3GHz). Visualmente existe una interferencia visible, un bajo rango dinámico y una resolución efectiva baja (480-600 líneas).

El sistema análogo se compone de tres componentes claves:

- **Cámara FPV analógica**
	- Convierte la imagen óptica en un flujo de video compuesto (CVBS).
	- Parámetros que importan:
		- Sensor CCD / CMOS
		- Resolución efectiva.
		- Rango dinámico.
		- WDR (Wide Dynamic Range)

- **VTX** - Video Transmiter
	- Toma la salida de la cámara y la *modula en RF* ([[1. Modularization]]) para enviarla por antena.
	- Algunos parámetros crícticos a tener en cuenta:
		- Potencia de salida (`mW`).
		- Frecuencia/carrier (Canales `5.8 GHz`).
		- Impedancia de antena (`50 Ω`).
		- Ganancia de antena (`dbi`).

- **Receptor** y **Googles**
	- Reciben la señal RF y la convierten de vuelta a video análogico.
	- Googles con sintonizador 5.8GHz múltiple.

| Component    | Model                     | Powers        | Notes                                                                        |
| ------------ | ------------------------- | ------------- | ---------------------------------------------------------------------------- |
| Camera       | *Foxeer Predator*         | -             | Sensor CMOS de alta sensibilidad, WDR y buen SNR                             |
| Camera       | *Foxeer Razer*            | -             | Sensor CMOS de alta sensibilidad, WDR y buen SNR                             |
| Camera       | *Foxeer HS1177*           | -             | Sensor CMOS de alta sensibilidad, WDR y buen SNR                             |
| Transmitters | *Foxeer TM25*             | 25/200/600 mW | Muy usado, ajustable                                                         |
| Transmitters | *TBS Unify Pro32 Nano*    | 25/200/600    | Referencia "pro"                                                             |
| Transmitters | *Rush Tank Ultimate Plus* | 25/200/600    | Gran filtrado, robusto                                                       |
| Googles      | *Fat Shark Recon v3*      | -             | Paneles LCD limpios, receptor 5.8GHz diversity (Dos antenas)                 |
| Googles      | *Skyzone SKY04X*          | -             | Receptores múltiples, paneles más grandes, soporta módulos si se necesitaran |
| Googles      | *Eachine EV800D*          | -             | Baratos, buena base de aprendizaje                                           |
| Antenna      | *Antenna Cloverleaf*      | -             | Para googles                                                                 |
| Antenna      | *Antenna Pagoda*          | -             | Para googles o drone                                                         |
| Antenna      | *Antenna dipolo* o *omni* | -             | Para tierra si estamos estáticos                                             |
> [!info] Powers
> - 25 `mW`: Corto alcance, interior.
> - 200 `mW`: Alcance urbano moderado.
> - 600 `mW`: Alto alcance en FPV casual.
> 
> A mayor potencia, más consumo y más calor (Hay que evaluar peso, disipación y batería).

###### Digital Video

El **video digital FPV** es un sistema de telecomunicaciones digitales completos donde se maneja una alta resolución (720p-1080p), con alto rango dinámico, lectura clara del entorno y grabación usable directamente desde el sistema.

---
# Command Control

El *control* (Radio tranmisor) es un *dispositivo de entrada humano* que:

- Genera señales digitales (Sticks, switches, knobs).
- Las codifica en un protocolo RC.
- Las transmite por RF o por USB (Simulador).

Para los simuladores:

- No se usa RF.
- La radio actúa como HID USB (Similar a un joystick tradicional).

Para que un control sea de una buena base gama media/alta, debe tener:

- Firmware abierto
	- **EdgeTX** (Estándar actual).
- Protocolo moderno
	- **ExpresLRS** (**ELRS**) integrado. 
- Gimbals decentes
	- Hall Effect (Sensor magnético).
- Conectividad USB nativa.

Hoy por hoy no tiene sentido empezar con protocolos viejos que no sean **ELRS**, ya que como mencionamos anteriormente este es OpenSource, tiene baja latencia, largo alcance y una enorme comunidad.

Recomendaciones para empezar: *RadioMaster Boxer ELRS*, *RadioMaster TX16S MKII ELRS* o *RadioMaster Zorro ELRS*.