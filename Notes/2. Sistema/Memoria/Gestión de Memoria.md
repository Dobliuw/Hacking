-----
- Tags: #teoria #sistemas #memoria
-----
# Memoria

La **memoria** es un área de almacenamiento dividido en unidades a las que se puede referenciara a través de una dirección. Es importante tener en cuenta que existen múltiples tipos de memoria, como la memoria **RAM**, **ROM**, memoria **Cache**, memoria **Virtual**, memoria de **Almacenamiento**, memoria de **BIOS**, etc.

----
# Gestor de memoria

El **Gestor de memoria** es un componente del Sistema Operativo que se encarga de las tareas relacionadas con la administración de la *Memoria Principal* (Memoria RAM).
- Asignación de Memoria RAM a los procesos que la solicitan. 
- Localización de espacios libres y ocupados.
- Aprovechamiento máximo de la memoria.

La memoria es una amplia tabla de datos, cada uno de los cuales cuenta con su propia dirección. Es importante tener en cuenta que para que los programas puedan ser ejecutados es necesario que estén cargados en memoria principal y que se almacene de modo permanente información necesaria en memoria secundaria (HDD, SSD, USB, etc).

----
# Particiones de memoria 

Las particiones de memoria son divisiones lógicas de la memoria RAM utilizadas para administrar y asignar espacio a programas en ejecución. Hay dos tipos principales de particiones de memoria:

- **Particiones Estáticas**: En este enfoque, la memoria se divide en particiones fijas de tamaños predeterminados. Cada partición puede albergar un programa. Este método puede llevar a un desperdicio de memoria si los programas son de diferentes tamaños y no se ajustan bien en las particiones.

- **Particiones Dinámicas**: En este enfoque, la memoria se divice en particiones de tamaño variable según la demanda. Esto permite un uso más eficiente de la memoria, ya que las particiones se asignan dinámicamente a programas a medida que se cargan y liberan. Sin embargo, esto puede ser más complejo de implementar.

-----
# Fragmentación

La fragmentación es la distribución desordenada y fragmentada de bloques de memoria en una región de almacenamiento, como la memoria RAM. Esta fragmentación puede tener un impacto negativo en el rendimiento y la eficiencia de un sistema informático. Existen dos tipos principales de fragmentación:

- **Fragmentación Interna**: Este tipo de fragmentación ocurre cuando se asigna más memoria de la necesaria para almacenar un proceso o programa en ejecución. Por ejemplo, en un sistema con particiones de memoria estática, si un rpograma ocupa solo una parte de la partición asignada, la diferencia entre el tamaño de la partciión y el tamaño del programa se considera fragmentación interna. La memoria en exceso asignada no se puede utilizar para otros fines, lo que resulta en una desperdicio de recursos.

- **Fragmentación Externa**: La fragmentación externa ocurre cuando hya suficiente memoria total disponible, pero no se puede asignar un bloque contiguo lo suficientemente grande para cargar un rpograma en ejecucción. Esto puede deberse a que hay suficiente memoria libre en términos absolutos, pero está dispersa en pequeños bloques no contiguos. La fragmentación externa puede provocar que un sistema sea incapaz de cargar programas que, en teoría, podrían ejecutarse debido a la falta de bloques de memoria contiguos suficientemente grandes.

La fragmentación puede afectar negativamente el rendimiento del sistema y la capacidad de asignar memoria de manera eficiente. Para abordar la fragmentación, los sistemas operativos y las aplicaciones utilizan diversas técnicas, como la compactación, la **paginación** y la **segmentación**.

----
# Paginación y Segmentación

La **paginación** es una técnica de gestión de memoria que divide la memoria en páginas de tamaño fijo. Los programas se dividen en páginas del mismo tamaño, y estas páginas se cargan en la memoria de manera independiente. La paginación permite una gestión eficiente de la memoria y facilita la asignación de bloques contiguos.  También facilita la implementacion de *memoria virtual* y el uso de la memoria secundaria (como el disco) para ampliar la memoria RAM.

Por otro lado, la **segmentación** es una técnica de gestión de memoria que divide la memoria en segmentos lógicos o secciones más grandes que pueden contener diferentes tipos de datos o componentes de un programa. Cada segmento puede crecer o contraerse de manera independiente. La segmentación es útil para dividir un programa en partes lógicas como el código, los datos, la pila ,etc. La gestión de segmentación puede ser más flexible que la paginación, pero requiere una gestión más compleja para asignar y liberar memoria. 

----
# Memoria Virtual y Swapping

La **memoria virtual** es una técnica que permite que un sistema operativo haga que un programa crea que tiene acceso a una cantidad de memoria física más grande de la que realmente está disponible. Se logra mediante la combinación de la memoria RAM y el almacenamiento en disco. La memoria virtual permite que múltiples programas se ejecuten en una máquina sin preocuparse por la cantidad física de RAM. Los programas puede acceder a una amplia memoria virtual, y el sistema operativo se encarga de cargar las partes necesarias en RAM a medida que se requieren. 

La traducción de las direcciones virtuales a reales es implementada por una **Unidad de Manejo de Memoria** (**MMU**). El sistema operativo es el responsable de decir qué partes de la memoria del programa es mantenida en memoria física. además mantiene las tablas de traducción de direcciones (Si se usa paginación la tabla se denomina *tabla de paginación*), que proveen las relaciones entre direcciones virtuales y físicas, para uso de la MMU.

El **Swapping** es una técnica de gestión de *memoria virtual* que implica mover bloques de datos entre la memoria principal (RAM) y la memoria secundaria (Generalmente el disco duro) según sea necesario. Cuando la memoria RAM se agota, el sistema operativo puede "intercambiar" bloques de datos entre la MP y la MS para otros programas. El *swapping* puede ralentizar el rendimiento del sistema si se realiza con frecuencia, ya que acceder a la memoria del disco es más lento que acceder a la RAM.