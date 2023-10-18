-----
- Tags: #teoria #sistemas #ejecutables
-----
# ELF - Executable and Linkable Format 

El formato **ELF (Executable and Linkable Format)** es un estándar amplicamente utilizado en sistemas operativos Unix y Linux para representar archivos ejecutables, bibliotecas compartidas y objetos compilados. Fue diseñado para ser un formato versátil y extensible que permite a los desarrolladores crear y distribuir software de manera eficiente y portátil.

----
# Estructura

Un archivo **ELF** consiste en una serie de **encabezados** y **secciones** que indican al **sistema operativo** cómo cargar y administrar el archivo en memoria. Recordemos que un archivo ELF se utiliza para proporcionar información esencial al sistema operativo sobre cómo organizar y ejecutar el cotenido del archivo. La información que el sistema necesita puede incluir:

- Referencias a bibliotecas compartidas que deben ser cargadas.
- Tablas de símbolos para resolución de símbolos.
- Segmentos y secciones que especifican cómo se debe cargar el archivo en memoria. (El sistema operativo mapeará el archivo en memoria en partes, no en su totalidad).

Es importante tener en cuenta que además, la **estructura** de un archivo ELF puede variar ya que dependiendo de si es un ejecutable, un objeto, una biblioteca compartida, etc. puede ser que el Program Header Table este previo el Section Header Table, esto de igual manera estara declarado en el ELF Header, donde el campo *e_phoff* (*Program Header Table Offset*) indicará la ubicación del inicio del Program Header Table así como el camp *e_shoff* (*Section Header Table Offset*) que inidicará la ubicación del inicio del Section Header Table. Teniendo en cuenta esto, la estructura del archivo ELF es la siguiente:

Imagén capturada de [[ELF_Format.draw]]
![[ELF_Format.png]]

------
# ELF Header (Elf32_Ehdr / Elf64_Ehdr)

Este es el Header principal de un archivo ELF. Contiene información fundamental, como el tipo de archvo (Ejecutable, objeto, biblioteca compartida, etc.), la arquitectura del procesador, la versión del formato, el punto de entrada y otros datos esenciales.

Definición de ELF Header en 32 bits:
```C
#include <elf.h>
#define EI_NIDENT (16)
 
typedef struct
{
  unsigned char e_ident[EI_NIDENT]; /* Número mágico y otros datos */
  Elf32_Half e_type; /* Tipo de fichero (ejecutable, biblio...) */
  Elf32_Half e_machine; /* Arquitectura */
  Elf32_Word e_version; /* Versión */
  Elf32_Addr e_entry; /* Punto de entrada */
  Elf32_Off e_phoff; /* Desplazamiento a la tabla de cabeceras de programa */
  Elf32_Off e_shoff; /* Desplazamiento a la tabla de cabeceras de sección */
  Elf32_Word e_flags; /* Flags específicos del procesador */
  Elf32_Half e_ehsize; /* Tamaño de la cabecera ELF */
  Elf32_Half e_phentsize; /* Tamaño de las cabeceras de programa */
  Elf32_Half e_phnum; /* Número de cabeceras de programa */
  Elf32_Half e_shentsize; /* Tamaño de las cabeceras de sección */
  Elf32_Half e_shnum; /* Número de cabeceras de sección */
  Elf32_Half e_shstrndx; /* Cabecera de sección que apunta a los nombres del resto de cabeceras */
} Elf32_Ehdr;
```


El comando **readelf** es una herramienta de línea de comandos que se utiliza para examinar y mostrar información detallada sobre archivos en formato ELF. 

Podemos visualizar el **ELF Header** haciendo uso del comando:

```bash
readelf -h {ELF_file}
```

Ejemplo: 

![[readelf_elf_header.png]]

----
# Program Header Table (Elf32_Phdr / Elf64_Phdr)

Esta es una tabla que consta de entradas de tipo **Elf32_Phdr** o **Elf64_Phdr**, donde cada entrada describe un segmento de programa específico dentro del archivo ELF. Cuando nos referimos a *describir un segmento de programa* nos referimos a proporcionar información sobre cómo se debe cargar y gestionar una parte específica del programa en la memoria durante su ejecución.

Esta tabla esta presente solo en archivos ejecutables y es una parte esencial de los archivos ELF, describe las segmentaciones de programa contenidas en el archiovo. A diferencia de los **Section Headers** que se utilizan para describir las secciones individuales del archivo (Como código, datos, etc.) los **Program Headers** se utilizan para describir segmentos de memoria que se cargan en la memoria durante la ejecución del programa. Estos segmentes pueden contener código ejecutable, datos, bibliotecas compartidas y otros recursos.

Para correr un programa, el Kernel cargar el **ELF Header** y el **Program Header Table** en memoria. Luego, carga el contenido especificado en el apatado **LOAD** de esta encabezado en memoria y también revisa si el intérprete es necesitado. Por último, se le da el control al propio ejecutable o al intérprete si está disponible. 

Definición de cada elemento **Program Header** en 32 bits, empiezan en el offset *e_phoff* del **ELF Header** y es un array con *e_phnum* de estos elementos:

```C
typedef struct {  
	uint32_t p_type;    /* Tipo de segmento */
	Elf32_Off p_offset; /* Desplazamiento dentro del archivo a partir del cual empieza */  
	Elf32_Addr p_vaddr; /* Dirección virtual donde el segmento debe cargarse */   
	Elf32_Addr p_paddr; /* Dirección física de carga, esto no es usado en la mayoría de sistemas */   
	uint32_t p_filesz;  /* Tamaño del segmento en el fichero, es el número de bytes que físicamente ocupa dentro del ELF */  
	uint32_t p_memsz;   /* Tamaño en memoria, cuando es mayor que el tamaño anterior, los bytes extra se suelen rellenar con ceros */  
	uint32_t p_flags;   /* Flags, indicando si el segmento se puede leer, escribir y/o ejecutar */
	uint32_t p_align;   /* Alineamiento, debe ser potencia de dos */   
} Elf32_Phdr;
```

Para listar la **Program Header Table** de un archivo ELF, podemos utilizar el siguiente comando:

```bash
readelf -l {ELF_file}
```

Ejemplo: 

![[readelf_program_table.png]]

----
# Sections

Luego del **Program Header Table**, vienen las secciones del archivo ELF. Las secciones son áreas lógicas dentro del archivo qeu contiene código, datos, símbolos, tablas de reubicación, información de depuración y otros tipos de datos. Cada sección tiene un propósito específico en el programa.

Algunas de las secciones habituales más importantes que existe en la mayoría de archivos ELF son:

- **.text**: Esta sección contiene el código ejecutable del programa. Es donde reside el código fuente compilado y se ejecuta cuando se inicia el programa. En esta sección se encuentra la lógica principal.
- **.data**: Esta sección almacena datos inicializados que el programa utiliza durante su ejecución. Esto puede incluir variables globales y datos estáticos que tienen un valor específico en el momento de la compilación.
- **.rodata**: Similar a la sección *.rdata* en el [[Portable Executable - Formato PE]], esta sección (*Read-only data*) almacena datos qeu son de solo lectura durante la ejecución. Estos datso suelen incluir cadenas constantes y otros valores que no deben modificarse.
- **.plt** y **.got**: Estas secciones están relacionadas con la resolución de símbolos y la vinculación dinámica. *.plt* (Procedure Linkage Table) contiene saltos de código que se utilizan para la resolución de símbolos en tiempo de ejecución, mientras que *.got* (Gloabl Offset Table) contiene punteros a funciones y variables globales que se resuelven en tiempo de ejecución.
- **.rel[a].text** y **.rel[a].data**: Estas secciones, como *.reloc* en PE, almacenan información de reubicación. Indican al enlazador dinámico cómo ajustar las direcciones de memoria de las secciones .text y .data para que el programa se pueda cargar en memoria correctamente.
- **.bss**: Aunque no aparece explícitamente en la **Section Table** la sección *.bss* es una sección común en ELF que almacena datos no inicializados. Esta sección no ocupa espacio en el archivoo, pero se reserva espacio en memroia para datos no inicializados como variables globales no inicializadas.

Definición de cada **Section** en 32 bits, empieza en *e_shoff* del **ELF Header** y contiene una cantidad determinada de secciónes declaradas en *e_shnum*:

```C
typedef struct {    
	Elf32_Word sh_name;      /* Nombre de sección (es un desplazamiento dentro de un array de caracteres) */ 
	Elf32_Word sh_type;      /* Tipo de sección */   
	Elf32_Word sh_flags;     /* Flags */  
	Elf32_Addr sh_addr;      /* Dirección virtual, si es que la sección forma parte de un segmento que se carga en memoria */ 
	Elf32_Off sh_offset;     /* Desplazamiento dentro del fichero */  
	Elf32_Word sh_size;      /* Tamaño en bytes */   
	Elf32_Word sh_link;      /* Índice de otra sección asociada, que quizá haga falta para procesar el contenido de esta */  
	Elf32_Word sh_info;      /* Información extra */   
	Elf32_Word sh_addralign; /* Alineamiento, debe ser potencia de dos */  
	Elf32_Word sh_entsize;   /* Tamaño de la entrada si la sección se refiere a una tabla */   
} Elf32_Shdr;
```

Para listar las secciones de un archivo ELF podemos hacer uso del comando:

```bash
readelf -S {ELF_binary}
```

Ejemplo:

![[readelf_section_table.png]]

----
# Section Header Table (Elf32_Shdr / Elf64_Shdr)

La **Tabla de Secciones** o **Section Header Table** es una parte fundamental del formato ELF. Contiene entradas de tipo **Elf32_Shdr** o **Elf64_Shdr** (**Sction Header**) que describen cada una de las secciones en el archivo, como nombres, tipos, tamaños, offsets y otros metadatos.

La información es usada durante el tiempo de enlace dinámico, justo antes de que el programa sea ejecutado. Los *linkers* enlazan el archivo con las bibliotecas compartidas que necesita para cargarlas en memoria. También esta sección contiene información que es usada por otros archivos para encontrar las definiciones simbolicas y referencias al programa.

La principal diferencia con el **Program Header** es que este se enfoca en describir cómo se debn cargar los segmentos de programa en la memoria durante la ejecución, mientras que los **Section Header** se enfocan en proporcionar información detallada sobre las secciones individuales del archivo ELF.

Para listar la **Section Header Table** de un binario podemos ejecutar el comando:

```bash
readelf -S {ELF_file}
```

Ejemplo:

![[readelf_section_table.png]]