# ESP32

El ESP32 es un microcontrolador de bajo costo y alto rendimiento desarrollado por Espressif Systems. Está diseñado para palicaciones de IoT, electrónica y automatización. Este dispositivo cuenta con un microprocesador de arquitectura Xtensa LX6 de doble núcleo (Aunque también existen versiones de un unico núcleo), conectividad Wi-Fi, Bluetooth integrada y una serie de interfaces de entrada y salida para conectar sensores, actuadores y otros dispositivos.

El ESP32 es conocido por su versatilidad y potencia en comparación con otros microcontroladores, gracias a sus caracteristicas claves:

- Conecitvidad Wi-Fi (802.11 b/g/n) y Bluetooth (4.2 y BLE).
- Amplia capacidad de memoria, con SRAM y flash integrados.
- Múltiples interfaces de comunicación, como UART, SPI, I2C e I2S.
- ADC (Analog-to-Digital Converter) y DAC (Digital-to-Analog Converter) para el procesamiento de señales analógicas.
- PWM (Pulse Width Modulation) para controlar motores, LEDs y otros dispositivos.
- Temporizadores y watchdog timers para gestionar tareas críticas.
- Capacidad de bajo consumo de energía, lo que lo hace ideal para aplicaciones que requieren funcionamiento continuo.

![[Pasted image 20250225165913.png]]

----
# Hardware Specification

La imagen a continuación muestra los pines y sus diferentes funciones en el ESP32 WROOM 32E.

![[Pasted image 20250225170624.png]]

- **Power Pins**:
	- *3V3*: Alimentación de 3.3V.
	- *GND*: Conexión a tierra.
	- *5V*: Entrada de voltadje de 5V (Regulada internamente).
- **GPIO (General Purpose Input/Output) Pins**:
	- Los pines GPIO pueden configurarse como entrada o salida según las necesidades de la aplicación.
	- Algunos pines específicos n oson tolerantesa 5V.
- **ADC and DAC Conversors**:
	- *ADC* (*Analog-to-Digital Converter*): Conversión de señales analógicas a digitales.
	- *DAC* (*Digital-toAnalog Converter*): Conversión de señales digitales a analógicas.
- **UART Interface** (**Serial Communication**):
	- *TX and RX*: Pines para transmisión y recepción serial.
- **SPI and I2C Communication Pins**:
	- *VSPI and HSPI*: Interfaces de comunicación SPI (Serial Peripheral Interface).
	- *I2c SDA and SCL*: Pines para comunicación I2C (Inter-Integrated Circuit).
- **Touch Input Pins**:
	- Los pines *TOUCH* permiten detectar cambios capacitivos y son útiles para crear interfaces táctiles.
- **Deep Sleep Pins**:
	- Pines específicos que permiten habilitar un modo de ahorro de energía para aplicaciones de bajo consumo.
