# Radio Frequencies

Las **Radiofrecuencias** (*RF*) son *ondas electromagnéticas* utilizadas para transmitir información sin necesidad de cables. Su rango se encuentra entre 3 kHz y 300 GHz, y son esenciales en tecnologías de comunicación como Wi-Fi, Bluetooth, redes móviles y radios bidireccionales.
##### Key characteristics

- Las RF transportan señales de audio, datos o video modulando la onda.
- Una frecuencia más alta implica una longitud de onda más corta y mayor capacidad para atravesar obstáculos.
- Comunicación inalámbrica, seguridad, sensores IoT y navegación (GPS).

-----
# Functionality

Los sistemas de RF como podría ser una Radio/Handy *Baofeng UV-82* funcionan con un principio básico:
##### Modulation

- **AM** (**Amplitude Modulation**): Modifica la amplitud de la onda portadora.
- **FM** (**Frecuency Modulation**): Modifica la frecuencia, usada en radios de dos vías por su resistencia al ruido.

##### Sender and Receiver

Un dispositivo emisor (Por ejemplo la radio) modula una señal de entrada (Voz) sobre una portadora. El receptor (Otra radio en la misma frecuencia a una determinada distancia) demodula esta señal para recuperarla y reproducir la entrada de la radio emisora (Voz).

##### Frecuency Band

- **VHF** (**Very High Frecuency**, *136.000* - *175.000 MHz*): Esta frecuencia es ideal para largas distancias en áreas abiertas (Como podrían ser descampados) y se ve facilmente afectada por obstáculos como edificios o elevaciones del terreno.
- **UHF** (**Ultra High  Frecuency**, *400.000* - *520.000 MHz*): Esta frecuencia recive una mejor penetración en e ntornos urbanos con obstáculos pero sacrificando el alcance, dado que este es menor comparado a VHF.

-----
# Duald Band and Application

Un dispositivo **dual band** (Como lo podría ser un *Baofeng UV-82*) indica que este puede operar en dos bandas diferentes (*VHF* y *UHF*).

Las ventajas de disponer de un dual band es que nos permite *monitorear dos frecuencias simultáneamente*, brindandonos flexibilidad para elegir la banda según el entorno. Existen múltiples escenarios donde esto podría ser aplicado, por ejemplo en un entorno de partidas de airsoft, podríamos usar una frecuencia dentro del rango de *136.000 MHz* y *174.000 MHz* (**VHF**) la cual podríamos utilizar en un entorno urbano, con edificios donde se esté llevando a cabo la partida y utilizar **UHF** pra *escanear frecuencias cercanas* e intentar *monitorear transmisiones enemigas*. 

----
# Predefined Channels and Scanning

Una radio como la *Baofeng UV-82* permite almacenar frecuencias en canales predefinidos para un acceso rápido. Esto es útil para no tener que sintonizar manualmente cada vez que cambiamos de canal.

Por otro lado, así como podemos configurar manualmente o acceder a frecuencias almacenadas en la memoria del dispositivo, también podríamos utilizar funcionalidades que suelen incluir estos dispositivos como lo es el escaneo de frecuencias. 

El escaneo de radiofrecuencias en este tipo de dispositivios suele ser un proceso controlado por el *firmware* del mismo, que realiza tareas específicas a nivel de hardware y software para buscar señales activas en un rango definido:

1. El dispositivo ajusta su oscilador local (*LO*, *Local Oscillator*), circuito electrónico que genera una señal de frecuencia fija, para recibir la señal de una frecuencia específica. Este ajuste es controlado por el sintetizador de frecuiencia, qeu genera la portadora necesaria para demodular la señal.

2. Una vez sintonizada una frecuencia, el receptor verifica si hay actividad (Presencia de señal) en ese canal. Esto se hace midiendo el nivel de señal de RF (*RSSI*, *Received Signal Strength Indicator*).

3. Si la señal es lo suficiente fuerte (Supera un umbral predeterminado), se considera activa y el dispositivo detiene el escaneo. Si no, pasa a la siguiente frecuencia.

##### Hardware Components Used

- **Local Oscillator** (**LO**): Es un cricuito electronico que genera una frecuencia portadora que el receptor necesita para sintonizar una frecuencia específica. El sintetizador controla el LO para ajustar la frecuencia en incrementos precisos (Normalmente en pasos de 12.5 kHz o 25 kHz, según el ancho de banda de la señal).

- **Frecuency Synthesizer**:  Es el encargado de generar las frecuencias precisas que la radio necesita para sintonizar. Funciona mediante un PLL (*Phase-Locked Loop*), que asegura que la frecuencia generada sea estable y exacta.

- **RF Signal Amplifier**: Una vez sintonizada, la señal recibida es amplificada y envíada al *demodulador* para extraer la información útil (Voz o datos).

- **Received Signal Strength Indicator**  (**RSSI**) **Measurement Circuit**: Este componente mide la intensidad de la señal recibida. Si el nivel es suficiente, el circuito informa al procesador para que detenga el escaneo.

- **Main Processor**: Un microcontrolador integrado que ejecuta el firmware controla el flujo de todo este proceso, es el encargado de:
	- Configurar el sintetizador de frecuencia.
	- Leer el valor de RSSI.
	- Decidir si detener o continuar el escaneo.