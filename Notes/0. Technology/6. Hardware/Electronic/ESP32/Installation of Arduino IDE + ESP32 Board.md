# Arduino IDE 

Como sabemos, **IDE** son las siglas de **Integrated Development Enviroment**, por lo que **Arduino IDE** es el entorno de desarrollo integrado oficial para programar placas arduino y otros microcontroladores, como el `ESP32` y `ESP8266`. Este software permite escribir, compilar y cargar códigos en las placas de manera senciall, utilizando un lenguaje basado en *C++*.

----
# Arduino IDE Alternatives

Si bien la instalación de Arduino IDE es sencilla, simplemente siguiendo la [documentación oficial](https://docs.arduino.cc/software/ide-v2/tutorials/getting-started/ide-v2-downloading-and-installing/), es importante saber que exdisten otras alternativas para utilizar en lugar de este IDE.

- *PlatformIO*: Es una extensión para Visual Studio Code potente, con autocompletado y gestión de dependencias.
- [Espressif IDF](https://idf.espressif.com/) (*ESP-IDF*): Framework oficial para programar el ESP32 en C/C++ con control total de hardware.
- *MicroPython*: Para programar el ESP32 en Python en lugar de C++. 

----
# Installing ESP32 Board into Arduino IDE 

Una vez descargado y seleccionado el path de instalación del IDE. Dentro de este podremos dirigirnos a la sección de *BOARDS MANAGER* y escribir **ESP32** para proceder con la instalación de todas las edependencias que requerirá el IDE para comunicarse y permitirnos comunicar de manera eficiente con esta o cualquier otra placa.

![[Pasted image 20250311120636.png]]

Otra manera alternativa de instalar la placa ESP32 dentro de nuestro IDE es yendo a *File* > *Preferences* y agregando en la sección de *Additional boards manager URLs* la URL del archivo JSON (https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json) que contendra todos los paquetes necesarios q ue utilizará la placa ESP32.