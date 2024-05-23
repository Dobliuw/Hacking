# Operative Systems 

Un **Sistema Operativo** (**OS**) es un software que actúa como intermediario entre los usuarios y el hardware del ordenador. Sus funciones principales incluyen la gestión de los recursos de hardware, la provisión de una interfaz de usuario y la ejecución y gestión de aplicaciones.

**Key Functions**
- *Processes management*: Controla la creación, ejecución y terminación de procesos.
- *Memory management*: Administra la memoria primaria o RAM, asignando y liberando espacio según sea necesario.
- *Files management*: Controla la creación, eliminación y acceso a archivos y directorios.
- *Devices management*: Maneja la comunicación entre el sistema y los dispostivos de hardware.
- *User Interfaces*: Proporciona una interfaz gráfica (GUI) o de línea de comandos (CLI) para que los usuarios interactúen con el sistema.

----
# Firmware

El **firmware** es un tipo de software que está programado en la memoria no volátil de un dispositivo de hardware. A diferencia del software regular que se almacena en discos duros o SSDs, el firmware está intergado directamente en el hardware y es esencial para el funcionamiento básico del dispositivo.

**Firmware Characteristics**:
- *Hardware Integration*: Está diseñado específicamente para interactuar con el hardware del dispositivo.
- *Persistence*: Almacenado en memoria no volátil (Como *ROM*, *EEPROM* o *Flash*), lo que significa que no se pierde cuando el dispostivo se apaga.
- *Updates*: Puede ser actualizado, aunque este proceso suele ser más complicado que actualizar software popular.
- *Basic Funcionality*: Proporciona las instrucciones básicas necesarias para que el hardware funcione y para que el software más complejo pueda interactuar con el hardware.

----
# BIOS and UEFI
#### BIOS (Basic Input/Output System)
La **BIOS** (**Basic Input/Output System**) es un firmware tradicional que inicializa el hardware del sistema y proporciona un entorno para que el sistema operativo se cargue. Se encuentre en un chip ROM en la placa base del equipo.

**Functions**:
- *Power-On Self-Test* (*POST*): Realiza pruebas de hardware al encender el sistema.
- *Hardware Initialization*: Configura y verifica los componentes de hardware.
- *Bootloader*: Localiza el cargador de arranque del sistema operativo en el disco y lo carga en la memoria.
- *System Configuration*: Proporciona una interfaz (Habitualmente de texto) para configurar opciones de hardware (Orden de arranque, configuración de periféricos, etc.)
###### BIOS Boot Process
- **System Power ON**:
	- Cuando encendemos una computadora, la BIOS se activa primero porque está almacenada en un chip ROM de la placa base/madre.
- **Power-On Self-Test** (**POST**):
	- La BIOS realiza una serie de pruebas de diagnóstico en el hardware (Memoria RAM, discos duros, dispositivos de entrada, etc.) para asegurar que todo funciona correctamente.
- **Hardware Initialization**:
	- La BIOS configura los componentes de hardware esenciales para que estén listos para ser usados por el sistema operativo.
- **Search Bootloader**:
	- La BIOS busca un dipositivo de arranque según el orden establecido en su configuración (Por ejemplo, primero disco duro, luego CD/DVD, luego USB, etc.).
	- La BIOS lee el sector de arranque principal (*MBR*) del dispositivo de arranque seleccionado. El MBR contiene el código del bootloader.
- **Load Bootloader**:
	- La BIOS carga el bootloader en la memoria y transfiere el control a éste.
	- El bootloader entonces carga el *kernel* del sistema operativo y empieza el proceso de arranque del sistema operativo.

#### UEFI (Unified Extensible Firmware Interface)
Por otro la **UEFI** (**Unified Extensible Firmware Interface**) es una intefaz moderna que reemplaza al BIOS. Ofrece más funcionalidades, mejor interfaz y soporte para características avanzadas.

**Functions**:
- *Grafical Interface*: Proporciona una interfaz gráfica más avanzada y amigable para la configuración del sistema.
- *GPT Support*: Permite el uso de tablas de partciones GPT, que soportan discos más grandes y más particiones.
- *Secure Boot*: Ayuda a proteger el proceso de arranque contra malware y software no autorizado.
- *Fast and Flexible*: Mejora los tiempos de arranque y ofrece mayor flexibilidad en la configuración y gestión del hardware.
- *BIOS Compatibility*: Puede emular la BIOS para mantener compatibilidad con sistemas operativos y hardware más antiguos.
###### UEFI Boot Process
- **System Power ON**:
	- Al encender el equipo, el firmware UEFI se activa primero porque está almacenado en un chip ROM o memoria flash en la placa base/madre.
- **Power-On Self-Test**:
	- Similar a la BIOS, UEFI realiza pruebas de diagnóstico en el hardware.
- **Hardware Initialization**:
	- UEFI configura lso componentes de hardware necesarios para el arranque.
- **Search Bootloader**:
	- UEFI busca un archivo de bootloader en la partición del sistema *EFI* (*ESP*) en un dispositivo de almacenamiento.
	- La *ESP* utiliza el sistema de archivos *FAT32* y contiene los archivos necesarios para el arranque del sistema operativo.
- **Load Bootloader**:
	- UEFI carga el archivo del bootloader especificado y transfiere el control a éste.
	- El bootloader entonces carga el *kernel* del sistema operativo y empieza el proceso de ararnqeu del sistema operativo.

| Characteristics | BIOS                             | UEFI                                            |
| --------------- | -------------------------------- | ----------------------------------------------- |
| Interface       | Texto                            | Gráfica y texto                                 |
| Partitions      | MBR (Máximo 2 TB, 4 particiones) | GPT (Más de 2 TB, hasta 128 particiones)        |
| Secure Boot     | No                               | Si                                              |
| Speed           | Lenta                            | Rápida                                          |
| Update          | Más compleja                     | Más sencilla y flexible                         |
| Compatibility   | Hardware y sistemas más antiguos | Hardware y sistemas modernos, puede emular BIOS |

----
# Partitions Tables (MBR vs GPT)

Las **tablas de particiones** son estructuras de datos en un disco duro o unidad de almacenamiento que describen cómo se divide el disco en particiones. Las particiones son secciones del disco que el sistema operativo puede gestionar de manera independiente, permitiendo así múltiples sistemas de archivos en un solo disco. Hay dos tipos principales de tablas de particiones, las cuales son **MBR** y **GPT**. 
#### MBR (Master Boot Record)

Master Boot Record = Registro de arranque Principal

**Principal Characteristics**:
- *Size Limit*: Soporte discos de hasta 2 TB.
- *Primary Partitions*: Hasta 4 particiones primarias.
- *Extendend and Logical Partitions*: Si se necesita más de 4 particiones, se puede crear una partición extendida que puede contener múltiples particiones lógicas.
- *Compatibility*: Es compatible con la mayoría de sistemas operativos, especialmente los más antiguos.

**Estructure**:
- *Starting Sector*: El MBR está ubicado en el primer sector del disco (Sector 0) y contiene el código de arranque principal y la tabla de particiones.
- *Starting Code*: El código de araranque es el primer software que se ejecuta cuando un equipo arranca.
- *Partitions Table*: Una estructura que contiene información sobre las pariciones del disco, como el tamaño y la ubicación de cada partición.

#### GPT (GUID Partition Table)

GUID Partition Table = Tabla de partición GUID

**Principal Characteristics**:
- *Size Limit*: Soporta discos de hasta 9.4 ZB (Zettabytes), mucho más grandes que los soportados por MBR.
- *Partitions*: Permite un número casi ilimitado de particiones (En la p´ractica, hasta 128 particiones en la mayoría de los sistemas),
- *Redundancy*: Incluye una tabla de particiones primaria y una copia de respaldo al final del disco para mayor seguridad.
- *Compatiblity*: Requiere firmware UEFI para arrancar desde discos GPT, aunque también puede usarse con BIOS en algunos casos.

**Estructure**:
- *Primary GPT Header*: Contiene información sobre la tabla de particiones y su ubicación.
- *Partitions Table*: Una lista de entradas que describen cada partición, incluyendo su tamaño, ubicación y un identificador único (GUID).
- *Backup Copy*: Al final del disco, GPT almacena una copia del header y de la tabla de particiones para redundancia.

| Characteristics      | MBR                                              | GPT                                              |
| -------------------- | ------------------------------------------------ | ------------------------------------------------ |
| Size Limit           | Hasta 2 TB                                       | Hasta 9.4 ZB                                     |
| Number of Partitions | Hasta 4 primarias (Más lógicas en una extendida) | Prácticamente ilimitadas (128 en práctica)       |
| Compatibility        | Amplia, especialmente con sistemas antiguos      | Requiere UEFI para arrancar                      |
| Redundancy           | No                                               | Sí, incluye una copia de respaldo                |
| Integrity            | Más susceptible a fallos                         | Más seguro, con CRC para verificar la integridad |
#### Utility and Relationated Commands

**In Linux**:
- `fdisk`: Usado principalmente para gestionar particiones *MBR*.
- `fdisk /dev/sda`
	- `n` para crear una nueva partición.
	- `d` para eliminar una partición.
	- `p` para imprimir la tabla de particiones.
	- `w` para escribir los cambios y salir.
- `gdisk`: Usado para gestionar particiones *GPT*.
- `gdisk /dev/sda`
	- `n` para crear una nueva partición.
    - `d` para eliminar una partición.
    - `p` para imprimir la tabla de particiones.
    - `w` para escribir los cambios y salir.
- `parted`: Puede gestionar tanto *MBR* como *GPT*.

**In Windows**:
- `Disk Management`: Herramienta gráfica para gestionar particiones.
- `diskpart`: Herramienta de línea de comandos para gestionar particiones.

-----
# Files Systems 

Un **sistema de archivos** (**Files System**) es una estructura lógica que un sistema operativo usa para controlar cómo se almacena y recuperan los datos en un dispositivo de almacenamiento. Sin un sistema de archivos, los datos colocados en un dispositivo de almacenamiento estarían en un solo bloque grande, sin forma de determinar dónde termina un dato y comienza el siguiente.

#### FAT32 (File Allocation Table 32)

**Characteristics**:
- *Compatibility*: Ampliamente compatible con casi todos los sistemas operativos (Windows, Linux, MacOS).
- *File Size Limit*: 4GB.
- *Partition Size Limit*: 8 TB.
- *Commoun Usage*: Unidades flash USB, tarjetas SD, discos duros externos.
- No soporta permisos de archivos avanzados.
- No es adecuado para grandes volúmenes de datos o archivos individuales grandes debido a sus límites de tamaño.
#### NTFS (New Technology File System)

**Characteristics**:
- *Compatibility*: Nativamente soportado por WIndows; puede ser lído y escrito en macOS con software adicional y en Linux con controladores adicionales.
- *File Size Limit*: 16 EB (Exabytes).
- *Partition Size Limit*: 256 TB.
- *Commoun Usage*: Partciiones de sistemas Windows, discos duros internos.
- Incluye funciones avanzadas como permisos de archivos, encriptación y registro de cambios. 
- Recuperación de errores y manejo de seguridad mejorado.
- Posee menor compatibilidad con sistemas operativos distintos a Windows sin software adicional.
- Más complejos que FAT32.
#### EXT4 (Fourth Extended Filesystem)

**Characteristics**:
- *Compatibility*: Principalmente utilizado en sistemas Linux.
- *File Size Limit*: 16 TB.
- *Partition Size Limit*: 1 EB (Exabyte).
- *Commoun Usage*: Particiones de sistemas Linux.
- Posee soporte para grandes volúmenes de datos.
- Funcionalidades como *journaling* (Registro de cambios) para mejorar la integridad de los datos.
- Aunque no es compatible con sistemas Windows y macOS de forma nativa.
- Así como también posee mayor sobrecarga de procesamiento debido a las características avanzadas.

Algunos otros sistemas de archivos son **APFS** (**Apple File System**), **HFS+** (**Apple Hierarchical File System Plus**), **Btrfs** (**B-tree File System**). 

| Characteristics      | FAT32                                                                                    | NTFS                                                           | EXT4                                                      |
| -------------------- | ---------------------------------------------------------------------------------------- | -------------------------------------------------------------- | --------------------------------------------------------- |
| Compatibility        | Windows, Linux, MacOS                                                                    | Windows, Linux y MacOS con Software o Controladores adicional. | Linux, Windows y MacOs con Software adicional.            |
| File Size Limit      | 4 GB                                                                                     | 16 EB                                                          | 16 TB                                                     |
| Partition Size Limit | 8 TB                                                                                     | 256 TB                                                         | 1 EB                                                      |
| Disadvantages        | No soporta funcionalidades avanzadas ni sirve para manejo de grandes volúmenes de datos. | Menor compatibilidad y mayor complejidad.                      | Menor compatibilidad y mayor sobrecarga de procesamiento. |

#### Utility and Relationated Commands

**In Linux**:

`mkfs`(*Make Filesystem*) = Crea un sistema de archivos en un dispositivo.
```bash
# Create a file system ext4 in /dev/sdx
mkfs.ext4 /dev/sdx 
# Create a file system NTFS in /dev/sdx
mkfs.ntfs /dev/sdx
```

`fsck`(*Filesystem Check*) = Comprueba y repara un sistema de archivos.
```bash
# Compare and repair file system in /dev/sdx
sudo fsck /dev/sdx
```

`mount` y `umount` = Monta y desmonda sistemas de archivos.
```bash
# Mount file system /dev/sdx in /mnt
sudo mount /dev/sdx /mnt
# Unmount /mnt
sudo umount /mnt
```

**In Windows**

`format` = Comando de línea para formatear volúmenes
```powershell
# Format unit E: with filesystem NTFS
> format E: /FS:NTFS
```

En resumen, en lo que involucra a **Tablas de Particiones** y **Sistemas de Archivos** puede generar un poco de confusión ya que en ambos se hablan de particiones, pero basicamente las tablas de particiones (MBR y GPT) definen cómo se divide el disco en secciones (Particiones), mientras que los sistemas de archivos (EXT4, FAT32, NTFS, etc) gestionan cómo se almacenan y recuperan los datos dentro de esas particiones.

Ejemplo:

1. Para crear una particion podríamos decidir en usar MBR o GPT (Dependiendo de si tenemos UEFI o BIOS) para dividir un disco de, por ejemplo, 500 GB, en particiones. Podríamos crear 2 particiones de 250GB por ejemplo.
2. Luego deberiamos elegir un sistema de archivos para formatear estas particiones (x2 250GB), por ejemplo, podríamos hacer que una partición disponga de la estructura lógica NTFS y otra EXT4.
3. Dentro de la partición NTFS, el sistema de archivos NTFS gestiona cómo se almacenan y organizan los archivos al igual que EXT4, con algunas pequeñas diferencias 

----
# CPU Architecture

Las **arquitecturas** de sistemas operativos también abarcan la forma en que el software se comunica con el hardware, y aquí es donde entrar las arquitecturas de *CPU*, como *x86*, *x86_64* (o *x64*), *ARM*, entre otras. Estas arquitecturas determinan la capacidad del procesador y cómo maneja las instrucciones y los datos.
#### x86
La arquitectura **x86** es una de las más antiguas y comunes, desarrollada por Intel. Es una arquitectura de 32 bits que ha sido la base de muchos procesadores de escritorio y portátiles.
- *Bits*: 32
- *Memory Direction*: Los procesadores x86 pueden direccionar hasta 4 GB de memoria RAM, esto se debe a que con 32 bits, se pueden crear `2^32` direcciones de memoria, lo que equivale a `4,294,967,296` (**4GB**).
- *Compatibility*: Altamente compatible con software antiguo y sistemas operativos diseñados para 32 bits.
- *Instructions*: Conjutno de instrucciones CISC (Complex INstruction Set Computing).

#### x86_64
La arquitectura **x86_64** o **x64**, es una extensión de la x86 y es capaz de manejar 64 bits. Fue introducida por AMD como AMD64 y posteriormente adoptada por Intel como Intel 64.
- *Bits*: 64
- *Memory Direction*: Los procesadores de x86_64 pueden direccionar teóricamente hasta 16 exabytes (`2^64` direcciones). Sin embargo, las implementeaciones actuales limitan esto a niveles más prácticos debido a restricciones físicas y de sistema operativo. Por ejemplo, muchos sistemas opertivos actuales limitan el soporte a varias terabytes de RAM, mucho más que los 4 GB de x86.
- *Compatibility*: Los procesadores x86_64 pueden ejecutar tanto software de 32 bits como de 64 bits. Esto es posible gracias a la compatibilidad hacia atrás (Backward compatibility) que permite que los preocsadores manejen instrucciones de 32 bits en un modo esepecail de compatibilidad.
- *Instructions*: Amplía el conjunto de instrucciones CISC de x86 con nuevas instrucciones y registros para mejorar el rendimineto y las capacidades del procesador.

#### ARM (Advanced RISC Machine)
La arquitectura **ARM** (**Advanced RISC Machine**) es una arquitectura de 32 bits y 64 bits utilizada principalmente en dispositivos móviles y embebidos debido a su eficiencia energética.
- *Bits*: 32 bits (ARMv7) y 64 bits (ARMv8).
- *Memory Direction*: ARMv7 puede direccionar hasta 4GB de RAM, mientras que ARMv8 puede direccionar mucho más.
- *Compatibility*: Utilizada en una amplia gama de dispositvios desde teléfonos inteligentes hasta servidores.
- *Instructions*: Conjunto de instrucciones RISC (Reduced Instruction Set Computing), que es más sencillo y eficiente energéticamente.

Algo que me ayudo personalmente a entender un poco más esto del direccionamiento de memorias, bits, CPU, etc. Es ver a la memoria *RAM* (*Random Access Memory*), una memoria voltail que ante la memoria de almacenamiento es mucho más rapida para el procesamiento de datos, como una "biblioteca", es esta buscamos guardar "libros" (*datos*), donde cada libro tiene un número de estante (*Dirección en memoria*). Una CPU (bibliotecario) que necesita encontrar y leer los libros

Resumiendo, simplifiquemos en que:

**Storage Space** / **Espacio de almacenamiento**
- Esto se refiere a cuánto espacio ocupa un programa o archivo en el disco duro o SSD.
- Un programa que ocupa, por ejemplo, 100 MB en disco, tiene su código y datos almacenados en esos 100MB en el SSD, HDD, etc.
**Memory Addressing Capability** / **Capacidad de Direccionamiento de Memoria**:
- Esto se refiere a la cantidad de memoria RAM que una CPU (Procesador) puede manejar o acceder directamente.
- En una arquitectura de 32 bits, la CPU puede direccionar hasta 4GB de memoria RAM.
- En una arquitectura de 64 bits, la CPU puede direccionar una cantidad de memoria mucho mayor (Teóricamente 16 exabytes, aunque en la práctica es mucho menos debido a las limitaciones físicas actuales).
**RAM and Processes** / **Memoria RAM y Procesos**:
- Es el espacio de trabajo temporal donde el sistema operativo y los programas cargan los datos y el código que necesistan mientras están en ejecución.
- Cada programa que se ejecuta encesita espacio en la RAM para sus datos y código.
