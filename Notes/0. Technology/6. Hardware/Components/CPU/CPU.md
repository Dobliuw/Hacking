# CPU (Central Processing Unit)

La **CPU** o **Unidad Central de Procesamiento** es el componente principal de un sistema infromático que realiza la mayoría de las operaciones de procesamiento de datos. Actúa como el "cerebro" del dispositivo, ejecutando instruccioens de programas y controlando otros componentes del sistema.

---
# Components

###### CPU Clock
El *reloj de la CPU* es un oscilador electrónico que genera pulsos a intevalos regulares. cada pulso representa un ciclo de reloj y sincroniza todas las operaciones dentro de la CPU.

El reloj se encarga de coordinar la ejecución de instrucciones y el flujo de datos en la CPU. Cada operación en la CPU se realiza en sincronía con estos pulsos de reloj, asegurando que las diferentes partes de la CPu trabajen juntas de manera ordenada.

###### Clock Frecuencies
La *frecuencia* del reloj es la velocidad a la que el reloj de la CPU genera puslso, medida en *Hertz* (*Hz*). En el contexto de las CPus, se suele expresar en *megahercios* (*Mhz*) o *gigaherzios* (*Ghz*).

Una mayor frecuencia de reloj significa que la CPU puede realizar más ciclos por segundo, lo que generalmente se traduce a una mayor capacidad de procesamiento. Sin embargo, el rendimiento real también depende de otros factores como la arquitectura y la eficiencia del pipeline.

###### CPU Cores
Los *núcleos* son una unidad de procesamiento independiente dentro de la CPU que puede ejecutar sus propias instruacciones. Las CPUs modernas suelen tener múltiples núcleos, lo que permite el procesamiento paralelo de múltiples tareas.

**Types**
- *Singe-Core*: CPU con un solo núcleo.
- *Multy-Core*: CPu con dos o más núcleos (Dual-core, Quad-core, Hexa-core, etc.), permitiendo la ejecución simultánea de múltiples hilos de procesamiento.

###### CPU Cache
El *cache* es una memoria rápida y de pequeño tamaño integrada en la CPU. Su función es almacenar temporalmente datos e instrucciones que la CPU usa con frecuencia, reduciendo así el tiempo de acceso comparado con la memoria principal (RAM).

**Cache Levels**
- *L1 Cache*: El más rápido y pequeño, directamente accesible por cada núcleo.
- *L2 Cache*: Más grande que el L1, puede ser dedicado a cada núcleo o compartido.
- *L3 Cache*: El más grande y lento, compartido entre todos los núcleos.

###### ISA (Instruction Set Architecture)
El *ISA* o Conjunto de Instrucciones de Arquitectura, es el conjutno de comandos que la CPU puede ejecutar. Define las operaciones disponibles, el formato de las instrucciones y los modos de direccionamiento.

**ISA Types**
- *CISC* (*Complex Instruction Set Computing*): Conjunto de instrucciones complejas
- *RISC* (*Reduced Instruction Set Computing*): Conjunto de instrucciones reducido y optimizado para la rapidez.

###### Pipeline
El *pipeline* es una técnica de procsamiento que divide la ejecución de instrucciones en varias etapas consecutivas. Esto permite que varias instrucciones se procesen simultáneamente en diferentes etapas del pipeline.

**Pipeline Stages**
- *Fetch*: Obtención de la instrucción desde la memoria.
- *Decode*: Decodificación de la instrucción.
- *Execute*: Ejecución de la instrucción.
- *Memory Access*: Acceso a la memoria si es necesario.
- *Wrtieback*: Escritura del resultado en un registro o en la memoria.

-----
# CPU Architecture

Las **arquitecturas** de sistemas operativos ([[Operative Systems Basics]]) también abarcan la forma en que el software se comunica con el hardware, y aquí es donde entrar las arquitecturas de *CPU*, como *x86*, *x86_64* (o *x64*), *ARM*, entre otras. Estas arquitecturas determinan la capacidad del procesador y cómo maneja las instrucciones y los datos.
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

