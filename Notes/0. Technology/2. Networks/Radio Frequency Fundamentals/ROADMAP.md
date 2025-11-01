#### 1. **Fundamentos de Radiofrecuencia**

- ¿Qué es una onda electromagnética?
- Frecuencia, longitud de onda, amplitud, fase.
- El espectro electromagnético: bandas de RF y su uso (AM/FM, VHF, UHF, ISM, etc.).
- Leyes/regulaciones y frecuencias reservadas vs. libres.
    

#### 2. **Modulación y Demodulación**

- Diferencia entre AM y FM (y sus variantes).
- Otras modulaciones: PM, QAM, FSK, PSK, ASK, GFSK, OOK, etc.
- Qué significa “modular” una señal y cómo afecta a la portadora.
- Ejemplos prácticos de transmisión y recepción.

#### 3. **Hardware de Radio y SDR*

- ¿Qué es un SDR? (Software Defined Radio)
- Arquitectura de un SDR: conversión analógica-digital, front-end RF, mezcladores, etc.
- Limitaciones de SDRs como el HackRF vs. radios tradicionales.
- Introducción al Portapack: hardware, firmware y sus módulos.
    

#### 4. **Protocolos y Servicios en el Aire**

- Introducción a protocolos de comunicación inalámbrica:
    - **FM/AM broadcast**
    - **Pagers**
    - **Radioaficionados**
    - **WiFi, Bluetooth, Zigbee (a nivel físico)*
    - **Sistemas de control remoto (RFID, llaves de autos, alarmas, sensores, etc.)**
- Cómo identificar protocolos y analizar su espectro.

#### 5. **Análisis de Señales**

- Uso de espectrogramas y waterfall
- Detección y filtrado de señales.
- ¿Qué son las señales analógicas vs. digitales? ¿Cómo las identifico?
- Herramientas de análisis: GQRX, SDR#, GNURadio (módulos básicos).

#### 6. **Práctica en Consola / CLI**

- Instalación y manejo de herramientas CLI para SDR: `hackrf_*`, `rtl_*`, `gqrx`, `gnuradio-companion`, etc.
- Ejercicios: sintonizar una FM, grabar y reproducir señales, analizar espectros.
- Scripts básicos para automatizar sintonización, grabación, reproducción.

#### 7. **Uso y Experimentos con Portapack**

- Navegación y funciones principales del Portapack.
- Uso de apps: spectrum analyzer, signal generator, demoduladores, grabación y replay, sniffing.
- Limitaciones de Portapack vs. CLI.

#### 8. **Introducción a Seguridad y Vulnerabilidades en RF**

- Por qué existen ataques en RF: debilidades en protocolos, falta de cifrado, etc.
- Ataques clásicos (teóricos): replay, jamming, sniffing, spoofing.
- Cómo surgen las vulnerabilidades: ¿por qué se pueden clonar llaves de autos, o abrir barreras, o hackear pagers?

#### 9. **Prácticas Éticas y Simulaciones de Ataques**

- Simulación de ataques controlados en tus propios dispositivos.
- Reglas y ética en hacking de RF: nunca interferir con comunicaciones ajenas ni servicios críticos.

#### 10. **Proyectos y Experimentación Avanzada**

- GNURadio avanzado: flujos personalizados.
- Decodificación de señales digitales.
- Construcción de antenas y mejoras de recepción.
- Integración con otros dispositivos: ESP32, Raspberry Pi, etc.