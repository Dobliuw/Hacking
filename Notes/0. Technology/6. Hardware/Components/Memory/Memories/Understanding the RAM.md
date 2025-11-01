-----
- Tags: #teoria #sistemas #memoria
-----
# RAM - (Random Access Memory)

La memoria RAM (Random Access Memory) es un tipo de memoria de acceso rápido que se utiliza en los or denadores y otros dispositivos electrónicos. Su función principal es proporcionar almacenamiento temporal de datos qeu el procesador necesita para llevar a cabo tareas y operaciones. 

La memoria RAM almacena temporalmente datos y rpogeamas que están en uso o que se acceden con frecuencia, lo que permite al procesador acceder a ellos de manera más rápida qeu si tuviera que recuperarlos desde un disco duro u otro medio de almacenamiento más lento. Esto acelear el rendimiento del sistema, ya que la lectura y escritura de datos en la RAM es mucho más rápida que en un disco duro.

Denominamos RAM (Random Access Memory) ya que se puede acceder a la información de una manera más rapida yendo directamente con una dirección al lugar en el que se encuentran los datos y recorriendo todos los datos.
![[ram_image.png|1090x790]]
Imagen ilustrativa de una memoria RAM DDR4

-----
# Canal y BUSES

Los **canales** y **BUSES** son la forma en la que se transfieren los datos entre la memoria y otros componentes, como el procesador y la placa madre.

- **Canales de memoria (Memory Channels)**: Los canales de memoria son vías de comunicación o caminos a través de los cuales los datos se transfieren entre la memoria RAM y el procesador. Los procesadores modernos admiten múltiples canales de memoria, que permiten una mayor velocidad de transferencia de datos. Utilizar varios canales de mmeoria al mismo tiempo puede mejorar significativamente el rendimiento del sistema, ya que se pueden trasmitir más datos simúltaneamente. La memoria RAM se instala en múdulos *DIMMs* uqe se conectan a estos canales de memoria que se componen de *BUSES*.

- **Buses de memoria**: Los buses de memoria son los conductos de datos y direcciones que conectan la memoria RAM con el procesador y otros componentes del sistema. Estos buses se utilizan para transmitir datos entre la CPU y la memoria. Los buses de memoria tienen una velocidad de reloj que determina la velocidad a la que los datos pueden ser transferidos entra la CPU y la mmeoria. A esto se lo conoce como el famoso *DDR RAM* (*Double Data Rate Random Access Memory*) utiliza **buses** que transmiten datos en el fanco ascendente y descendente del ciclo del reloj.

Podemos resumir diciendo que los **canales** son vías de comunicación entre los componentes del sistema, los cuales se componen de **BUS** (**Buses en plural**), que son pequeños "cables" (Pistas de cobre) que conducen la electricidad (0s y 1s), lo que se demonida como que son los encargados de conducir los datos.

Imagen de un buses.
![[bus_image.png]]

-----
# DIMM - (Dual In-line Memory Module)

Antes de hablar de los **DIMM**, ya entendiendo de que tratan los *Canales* y los *Buses*, es importante tener en cuenta que los **DIMM** se comunican con el *procesador* utilizando un canal que utiliza 3 tipos de buses distintos, el bus de **Direcciones**, bus de **Control**, bus de **Reloj** y bus de **Datos**.

- **Buses de Direcciones (Address Bus)**: Estos buses, son 17 "cables" (Pistas de cobres), por lo que son 17 bits, es decir números desde el 0 al 131.071, que indican las direcciones en memoria de donde se recuperarán los datos o se alojarán (Acción que será determinada por los *Buses de Control*).

![[address_bus.png]]

- **Buses de Control (Control Bus)**: Estos buses de control son responsables de gestionar y coordinar las operaciones de lectura y escritura en la memoria RAM. Estos buses transmiten señales de control que indican al sistema cuiándo se debe leer o escribir datos.

![[control_bus.png]]

- **Bus de Reloj (Clock Bus)**: Señal eléctrica que marca el ritmo o la velocidad de operación de un sistema informático. El bus del reloj es el generador de pulsos elécticosd qeu sincroniza y coodina las operaciones de todos los componentes del sistema.

![[clock_bus.png]]

- **Buses de Datos (Data Bus)**: Los buses de datos son utilizados para la transferencia de los propios datos entre la memoria RAM y la CPU. Estos buses transportan los datos que se leen desde la memoria  oque se escriben en ella. Estos buses son de 64 Bits y aca es donde entra en juego nuestro nuevo concepto **DIMM**, así como también el concepto de **SIMM**. 

![[data_bus.png]]

El **DIMM** o **Módulo de Memoria de Doble Línea** en español, se refiere a un tipo de módulo de memoria utilizado en computadoras y otros dispositivos electrónicos para ampliar la memoria RAM. Los DIMM son una forma común de empaquetar y conectar chips de memoria en placas de circuito impreso que luego se insertan en las ranuras de memoria de una placa madre o una placa base de computadora.

Los DIMM son una evolución de los **SIMMns** (**Single In-Line Memory Modules**), que solo tenía contacto de un lado de la memoria, lo que limitaba la memoria teniendo un menor rendimiento.

Básicamente en el DIMM contamos con estos "lectores" de doble cara (Tanto de frente como detras de la memoria), mientras que en los SIMM esto no erá así y solo contabamos con estos lectores de una sola cara de la memoria, por esto con los SIMM teníamos 32 bits de lectura y ahora con los DIMM contamos con 64 bits.

Imagen del SIMM.
![[SIMM_image.png]]

Imagen del DIMM.
![[DIMM_image.png]]

De aquí su nombre de DIMM (**Double In-Line Module Memory**).

----
# Dual Channel

El **Dual Channel** (**Canal Doble**) es una tecnología utilizada en las placas madre para mejorar el rendimiento de la memoria RAM. Esta tecnología permite a la memoria RAM operar en dos canales de forma simultánea, lo que aumenta la velocidad de transferencia de datos entre la memoria y el procesador. En lugar de accedera a la memoria a través de un solo canal, el dual channel permite la transferenica paralela de datos a través de dos canales de memoria.

![[dual_channel_image.png]]

-----
# Reloj y DDR

El **reloj** es un funcionalidad que posee el procesador y es la frecuencia o velocidad de reloj del sistema (Reloj de CPU o Reloj Central). Esta es una señal eléctrica que oscila a una frecuencia constante y regula la velocidad a la que el procesador ejecuta instrucciones y realiza operaciones.

El reloj del procesador se mide en hercios (Hz) y generalmente se expresa en múltiplos como megahercios (MHz) o Gigahercios (GHz). Por ejemplo, si tenemos un procesador que funciona a 3.0 GHz, significa que el reloj oscila a 3.000.000.000 de veces por segundo.

La velocidad del reloj del procesador está relacionada con la velocidad de acceso a la memoria RAM. Los procesadores realizan muchas operaciones que requieren el acceso a datos almacenados en la memoria RAM. Ya que es este el que indica con que frecuencia la memoria RAM deberá revisar los datos entrantes. 
Gracias a esto, es que la memoria RAM recibe el nombre de **SDRAM** (**Synchronus Dynamic Random-Acces Memory**). 

En un pasado, cuando la frecuencia emitida del reloj (Siendo esta la orden para la reelectura de datos) se apagaba, era cuando se completaba un ciclo de datos, pero cambiaron el sistema para que esto suceda cuando sube o baja la frecuencia, de esta manera nace el famoso **DDR** (**Doble Data Rate**).

![[pre_DDR.png]]

En cambio, con **DDR** aumentamos la velocidad, conocido también como **Pumping**, lo que permite transmitir datos dos veces por ciclo del reloj (DDR).

![[DDR_image.png]]