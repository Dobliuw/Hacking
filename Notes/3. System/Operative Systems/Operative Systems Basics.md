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
# CPU Architecture

Este es un tema previamente explicado en [[CPU]] por lo cual no voy a redundar en el tema, pero esto es algo a tener en cuenta dentro del apartado de los Sistemas Operativos.

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

![[mbr_excalidraw_examples.png]]

En este ejemplo podemos tener en cuenta...

- **Tamaño**: MBR solo puede gestionar discos de hasta 2TB. Esta es una limitación debido a la forma en que se almacenan las direcciones de los bloques en el MBR.
- **Número de Particiones**: MBR permite un máximo de 4 particiones *primarias*. Si se necesitan más particiones, una de estas particiones primarias puede ser convertida en una partición extendida, que puede contener múltiples particiones lógicas.

- **Particiones Primarias**: Puedes tener hasta 4 particiones primarias. En nuestro ejemplo, se representa un disco de 2TB dividido en 4 particiones primarias de 500GB cada una. Esto es correcto y muestra una posible división del disco.
- **Partición Extendida**: Si solo se utilizan 3 particiones primarias, la cuarta puede ser una partición extendida. En nuestro ejemplo, una partición extendida de 1TB contiene 8 particiones lógicas de 125GB cada una. Esto muestra cómo una partición extendida puede contener múltiples particiones lógicas (Únicamente almacenando datos en su interior).

Por ejemplo, tomando este último caso, podríamos tener en linux:

- **Tamaño del Disco**: 2TB
- **Particiones**:
    - 3 Particiones Primarias: 333GB cada una (/dev/sda1, /dev/sda2, /dev/sda3)
    - 1 Partición Extendida: 1TB (/dev/sda4)
        - Contiene 8 Particiones Lógicas: 125GB cada una (/dev/sda5, /dev/sda6, etc.)


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
# Kernel

El **Kernel** es el núcleo del sistema operativo que gestiona las interacciones entre el hardware y el software de un sistema. Hay varios tipos de kernels, cara uno con sus propias características y ventajas.

**Type of Kernels**
- *Monolithic Kernel*: Todo el sistema operativo funciona en un único especio de memoria (Kernel Space). Ejemplos incluyen a Linux y Unix.
- *Microkernel*: el núcleo del sistema operativo está reducido a las funcionalidades más básicas (Gestión de procesos, comunicación inter-procesos, etc.) y el resto del sistema operativo se ejecuta en un espacio de usuario. Ejemplo: Minix.
- *Hybrid Kernel*: Combina elementos de los kernels monolíticos y microkernels. Ejemplos inlcuyen Windows NT y macOS.

**Kernel Functions**
- *Process Management*: Gestiona la creación, ejecución y terminación de procesos.
- *Memory Management*: Administra la memoria RAM del sistema.
- *Device Management*: Gestiona los controladores de dispositivos para interactuar con el hardware.
- *File System Management*: Proporciona una interfaz para la creación, lectura, escritura y eliminación de archivos.

----
# Virtualization

La **virtualización** es una tecnología que permite crear múltiples entornos de ejecución aislados sobre un único hardware físcio. Esto se logra mediante la creación de máquinas virtuales (VMs), cada una de las cuales actúa como un sistema completo con su propio sistema operativo, aplicaciones y recursos dedicados.

**Hypervisor**:
- Un *hypervisor*, también conocido como monitor de máquina vritual (VMM), es un software, firmware o hardware que crea y ejecuta máquinas virtuales. Un hypersvisor permite que un host físico ejecute múltiples VMs, compartiendo los recursos físcios de manera eficiente.
- *Hypervisors Types*:
	- *Type 1* (*Bare Metal*): Corre directamente sobre el hardware físico, sin necesidad de un sistema operativo host. Proporciona un alto rendimiento y es comúnmente usado en entornos de producción empresarial, por ejemplo VMware ESXi, Microsoft Hyper-V o Xen.
	- *Type 2* (*Hosted*): Corre sobre un sistema operativo host, actuando como una aplicación más en el sistema opeartivo. Es más fácil de instalar y usar en entornos de escritorio o de desarrollo, por ejemplo VMWare Workstation y Oracle Virtualbox.
- Las *funcionalidades* de este son la gestión de la creación, ejecución y monitorización de las máquinas virtuales, incluyendo la asignación de recursos como CPU, memoria y dispostivios de almacenamiento.

Mencionamos a las VMs, pero.. que son? Una VM (Virtual Machine) es un contenedor de software que puede ejecutar un sistema opperativo y aplicaciones como si fuera un computadora física completa. Las VMs son independientes y están aisladas unas de otras.

**VM Componentes**:
- *Guest Operative System*: El sistema operativo que corre dentro de la VM.
- *Virtualized Hardware*: Incluye CPU virtual, memoria RAM virtual, discos duros virtuales y adaptadores de red virtuales.

El uso de esta tecnología nos permite aprovechar capacidades de la misma como lo son el asilamiento, dado que como mencionamos, están aisladas entre sí, lo que aumenta la seguridad y la estabilidad y capacidades como la flexibilidad dado que se nos permite ejecutar diferentes sistemas operativos y versiones en un mismo hardware.

**Memory Management**
- *Overcommitment*: El hypervisor puede asignar más memoria virtual a las VMs de la que físicamente está disponible en el host. Esto se basa en la suposición de que no todas las VMs usarán toda su memoria asignada al mismo tiempo.
- *Ballooning*: Técnica ut8ilizada por los hypervisores para recuperar memoria de las VMs cuando el host necesita más recursos. Un controlador de ballooning instalado en la VM devuelve memoria no utilizada al host.
- *Swapping*: Si la memoria física del hos se agota, el hypervisor puede usar almacenamiento secundario (Como discos duros) para suplir la demanda de memoria, aunqeu esto reduce el rendimineto debido a la mayor latencia del disco comparada con la RAM.

**Storage Management**
- *Virtual Disk*: Cada Vm tiene un o más discos virtuales (Por ejemplo, archivos .vmdk o .vdi) que simulan un disco físico. Estos archivos residen en el almacenamiento del host y pueden ser fijos o dinámicos.
- *Thin Provisioning*: Técnica que permite asignar más espacio de almacenamiento virtual del que está realmente disponible en el host, permitiendo una utilización más eficiente del espacio físico disponible.
- *Snapshots*: Capturas del estado de una VM en un momento específico, permitiendo revertir cambios o restaurar la VM a un estado anterior. ütiles para pruebas de softwares, análisis de malware, etc. y recuperación rápida de errores.

**Networking**
- *Virtual Switches*: Componentes virtuales que permiten que las VMs se comuniquen entre sí y con el exterior. Pueden configurarse para emular distintos tipos de topologías de red.
- *VLANs*: Segmentación de redes virtuales para mejorar la seguridad y el rendimineot. Las VLANs permiten separar el tráfico de red de diferentes VMs incluso cuando comparten el mismo hardware físico.

**Performance Optimization**
- *CPU Allocation*: Distribución de núcleos de CPU físicos entre las VMs. Puede incluir técnicas de afinidad de CPU para mejorar el rendimiento al aseguriar que ciertas VMs usen CPUs específicas.
- *NUMA* (*Non-Uniform Memory Access*): Optimización que respeta la arquitectura física del host, minimizando las latencias al asegurar que las Vms usen memoria y CPUs localizados en el mismo nodo NUMA.
- *I/O Optimization*: Uso de controladores paravritualizados (Como Virtio en KVM) para mejorar el rendimineto de entrada/salida en VMs, reduciendo la sobrecarga de la virtualización.

----
# GRUB (Grand Unified Bootloader)

**GRUB** es un gestor de arranque (*Bootloader*) utilizando principalmente en sistemas operativos Unix-like, como Linux. Su función principal e cargar el sistema operativo en la memoria y transferirle el control durante el proceso de arranque del sistema.

- *GRUB Legacy*: Era la versión original de GRUB, utilizada ampliamente antes de 2010.
- *GRUB 2*: La versión actual, que incluye ejoras significativas en cuanto a funcionalidad, modularidad y soporte para múltiples sistemas operativos.

GRUB permite al usuario seleccionar entre múliples sistemas operativos instalados en el mismo sistema. Esto es útil en configuraciones de dual o multiple boot.

A su vez, también permite configurar opciones específicas para el arranque del ssitema operativo, como parámetros del kernel, modo de recuperación y otros. Soporta una amplia variedad de sistemas de archivos, lo que le permite leer los archivos de configuración y el kernel de diferentes tipos de particiones.

**GRUB Config Files**
`grub.cfg`
- *Path*: Generalmente en `/boot/grub/grub.cfg`.
- Contiene las configuraciones del menú de GRUB, incluyendo las entradas de menú para diferentes sistemas operativos y opciones de arranque.

`grub.d` (Directory)
- *Path*: `/etc/grub.d/`.
- Contiene scripts que generan las entradas de menú en `grub.cfg`. Cada script en este directorio corresponde a una entrada en el menú de GRUB.

`grubenv`
- *Path*: Generalmente en `/boot/grub/grubenv`.
- Un archivo de ambiente que almacena variables persistentes usadas por GRUB, como la entrada de menú predeterminada para el próximo arranque.

**GRUB Commands**
- `update-grub`: Genera el archivo `grub.cfg` a partir de los scripts en `/etc/grub.d/` y la configuración en `/etc/default/grub`.
- `grub-install`: Instala GRUB en el dispositivo de arranqeu (MBR o partición específicada).
- `grub-mkconfig`: Similar a `update-grub`, genera el archivo de configuración GRUB.

**Commoun changes**
Algunos cambios relacionados al GRUB se pueden llevar a cabo editando lo scripts en `/etc/grub.d` o el archivo `/etc/default/grub`.
- Para cambiar el sistem operativo predeterminado deberiamos editar la variable **GRUB_DEFAULT** encontrada en el directorio `/etc/default/grub`.
- Para cambiar el tiempo de espera del menú habría que modificar la variable **GRUB_TIMEOUT** en el directorio mencionado anteriormente.
- De igual manera, para añadir parámetros del kernel deberiamos modificar la línea **GRUB_CMDLINE_LINUX_DEFAULT**.

El GRUB es capaz de trabajar tanto con *MBR* (*Master Boot Record*) como con *GPT* (*GUID Partition Table*). Estas tablas de particiones organizan la disposición de particiones en el disco duro.
A su vez, el bootloader GRUB puede manejar varios sistemas de archivos como *EXT4*, *FAT32* y *NTFS*. Tanto si utilizamos configuraciones de *Dual Boots* o *Multiple Boots*, así como si unicamente contamos con un *único sistema operativo* basado en Linux, el GRUB o nos permitira seleccionar entre múltiples sistemas operativos instalados en el mismo sistema, por ejemplo un Debian y Windows (Si fuera el caso) como podría encargarse únicamente de cargar el sistema operativo instalado, así como mostrar una pantalla inicial que permite seleccionar opciones avanzadas, como modos de recuperación o configuración del firmware *BIOS* (*Basic Input/Output System*) *UEFI* (*Unified Extensible Firmware Interface*).

