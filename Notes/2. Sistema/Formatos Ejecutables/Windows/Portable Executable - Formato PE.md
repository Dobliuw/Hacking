-----
- Tags: #teoria #sistemas #ejecutables
-----
# Portable Executable

**PE** prviene de **Portable Executable**, el cual es un formato de archivo para ejecutables utilizados en los sistemas operativos Windows, se basa en el formato de archivo *COFF* (Common Object File Format).

No solo los arhciovs *.exe* son archivos PE, las bibliotecas de enlaces dinámicos (*.dll*), los módulos del kernel (*.srv*), las aplicaciones del panel de control (*.cpl*) y muchos otros también son archivos PE. Un archivo PE es una estructura de datos que contiene la información necesaria para que el cargador del sistema operativo pueda cargar ese ejecutable en la memoria y ejecutarlo.

----
# [Estructura](http://www.openrce.org/reference_library/files/reference/PE%20Format.pdf)

Un archivo **PE** consiste de una serie de **headers** y **secciones** que indican al **enlazador dinámico** [^1] cómo asignar el archivo en memoria. 
Recordemos que un archivo de formato PE sirve para decirle a enlazadores dinámicos qué información necesitan para administrar el código ejecutable empaquetado. La información que requiere el sistema se puede mencionar como:

- Referencias a DLLs a importar.
- Importar/Exportar tablas de API.
- Cuánto espacio de memoria reservar. (En la memoria irán el código, los datos y los recursos que necesitará el proceso en el sistema. El PE nunca se mapea entero, solo por partes).

Teniendo en cuenta esto, la **estructura** de esta información se puede encontrar de la siguiente manera:

Imagén de capturada del [[PE_Format.draw]].
![[PE_Format.png]]

-----
####  **DOS**[^2] Header:
Cada arachivo PE comienza con una estructura de *64 bytes* de largo llamada DOS Header, es lo que hace que el archivo PE sea un ejecutable de MS-DOS.

**IMAGE**[^3] del DOS Header
```C
typedef struct _IMAGE_DOS_HEADER { 
0x00 WORD e_magic; 
0x02 WORD e_cblp; 
0x04 WORD e_cp;
0x06 WORD e_crlc; 
0x08 WORD e_cparhdr; 
0x0a WORD e_minalloc; 
0x0c WORD e_maxalloc; 
0x0e WORD e_ss; 
0x10 WORD e_sp; 
0x12 WORD e_csum;
0x14 WORD e_ip;
0x16 WORD e_cs;
0x18 WORD e_lfarlc; 
0x1a WORD e_ovno; 
0x1c WORD e_res[4];
0x24 WORD e_oemid; 
0x26 WORD e_oeminfo;
0x28 WORD e_res2[10];
0x3c DWORD e_lfanew; 
} IMAGE_DOS_HEADER, *PIMAGE_DOS_HEADER;
```

Los miembros más importantes de esta estructura son *e_magic* y *e_lfanew*.  Siendo el *e_magic* 2 bytes con el valor *0x5A4D* (*MZ*) y *e_lfanew* un valor de 4 bytes que contiene el **offset** hasta el inicio del NT Header (Siempre *e_lfanew* se encuentra en el **offset** *0x3C*).

----
#### DOS Stub
El código auxiliar de DOS, es un pequeño ejecutable compatible con MS-DOS 2.0 que simplemente imrpime un mensaje de error que dice **This Program Cannot Run in DOS Mode** y suele ocupar *57 bytes*.

----
#### NT Headers
Parte fundamental de la estructura de los archivos PE. Este encabezado proporciona información esencial sobre la organización y el contenido del archivo ejecutable, lo que permite al sistema operativo y a otros programas comprender cómo cargar y ejecutar el archivo de manera adecuada. 

IMAGE del NT Headers x86
```C
typedef struct _IMAGE_NT_HEADERS { 
0x00 DWORD Signature;
0x04 _IMAGE_FILE_HEADER FileHeader; 
0x18 _IMAGE_OPTIONAL_HEADER32 OptionalHeader; 
} IMAGE_NT_HEADERS32, *PIMAGE_NT_HEADERS32;
```

IMAGE del NT Headers x64
```C
typedef struct _IMAGE_NT_HEADERS { 
0x00 DWORD Signature;
0x04 _IMAGE_FILE_HEADER FileHeader; 
0x18 _IMAGE_OPTIONAL_HEADER64 OptionalHeader; 
} IMAGE_NT_HEADERS64, *PIMAGE_NT_HEADERS54;
```

Este Header es esencial ya que incorpora otros dos Headers que son estructuras de datos (*FileHeader* y *OptionalHeader*).
##### **File Header**: Header de archivo COFF estándar. Contiene información sobre el archivo PE.

IMAGE del File Header
```C
typedef struct _IMAGE_FILE_HEADER { 
0x00 WORD Machine;
0x02 WORD NumberOfSections;
0x04 DWORD TimeDateStamp;
0x08 DWORD PointerToSymbolTable; 
0x0c DWORD NumberOfSymbols;
0x10 WORD SizeOfOptionalHeader;
0x12 WORD Characteristics; 
} IMAGE_FILE_HEADER, *PIMAGE_FILE_HEADER;
```

Los miembros más importantes de esta estructura son:
- **NumberOfSections**: El number de secciones en el archivo PE.
- **Characteristics**: Flags que especifican ciertos atributos sobre el archivo ejecutable, como si es una DLL o una aplicación de consola.
- **SizeOfOptinalHeader**: El tamaño del siguiente Optional Header

##### **Optional Header**: El Header más importante en los NT Headers, su nombre es Optional Header porque algunos archivos, como los archivos objeto, no lo tienen, es necesario para los archiuvos de imagen (Archivos como .exe). Este encabezado proporciona información importante al cargador del sistema operativo.


IMAGE del Optional Header
```C
typedef struct _IMAGE_OPTIONAL_HEADER { 
0x00 WORD Magic; 
0x02 BYTE MajorLinkerVersion; 
0x03 BYTE MinorLinkerVersion;
0x04 DWORD SizeOfCode; 
0x08 DWORD SizeOfInitializedData;
0x0c DWORD SizeOfUninitializedData;
0x10 DWORD AddressOfEntryPoint; 
0x14 DWORD BaseOfCode; 
0x18 DWORD BaseOfData; 
0x1c DWORD ImageBase; 
0x20 DWORD SectionAlignment;
0x24 DWORD FileAlignment;
0x28 WORD MajorOperatingSystemVersion; 
0x2a WORD MinorOperatingSystemVersion;
0x2c WORD MajorImageVersion; 
0x2e WORD MinorImageVersion; 
0x30 WORD MajorSubsystemVersion; 
0x32 WORD MinorSubsystemVersion;
0x34 DWORD Win32VersionValue;
0x38 DWORD SizeOfImage; 
0x3c DWORD SizeOfHeaders; 
0x40 DWORD CheckSum; 
0x44 WORD Subsystem; 
0x46 WORD DllCharacteristics;
0x48 DWORD SizeOfStackReserve;
0x4c DWORD SizeOfStackCommit;
0x50 DWORD SizeOfHeapReserve;
0x54 DWORD SizeOfHeapCommit; 
0x58 DWORD LoaderFlags;
0x5c DWORD NumberOfRvaAndSizes;
0x60 _IMAGE_DATA_DIRECTORY DataDirectory[IMAGE_NUMBEROF_DIRECTORY_ENTRIES];  // IMAGE_NUMBEROF_DIRECTORY_ENTRIES = 16
};
```

-----
#### Data Directory 
Este apartado se encuentra dentro del *Optional Header*, y las entradas de este Array de un total de *IMAGE_NUMBEROF_DIRECTORY_ENTRIES* = *16* posiciones apunta a diferentes tablas y estrucutas de datos importantes que se almacenan e nsecciones específicas del archivo PE.

Cada posición del array representa un Data Directory especifico que puede incluir algo de data de la **PE Section** o **Data Table**

IMAGE de cada Data Directory
```C
typedef struct _IMAGE_DATA_DIRECTORY { 
0x00 DWORD VirtualAddress; 
0x04 DWORD Size; 
} IMAGE_DATA_DIRECTORY, *PIMAGE_DATA_DIRECTORY;
```

Indices del Array
```C
define IMAGE_DIRECTORY_ENTRY_EXPORT          0   // Export Directory
define IMAGE_DIRECTORY_ENTRY_IMPORT          1   // Import Directory
define IMAGE_DIRECTORY_ENTRY_RESOURCE        2   // Resource Directory
define IMAGE_DIRECTORY_ENTRY_EXCEPTION       3   // Exception Directory
define IMAGE_DIRECTORY_ENTRY_SECURITY        4   // Security Directory
define IMAGE_DIRECTORY_ENTRY_BASERELOC       5   // Base Relocation Table
define IMAGE_DIRECTORY_ENTRY_DEBUG           6   // Debug Directory
define IMAGE_DIRECTORY_ENTRY_ARCHITECTURE    7   // Architecture Specific Data
define IMAGE_DIRECTORY_ENTRY_GLOBALPTR       8   // RVA of GP
define IMAGE_DIRECTORY_ENTRY_TLS             9   // TLS Directory
define IMAGE_DIRECTORY_ENTRY_LOAD_CONFIG    10   // Load Configuration Directory
define IMAGE_DIRECTORY_ENTRY_BOUND_IMPORT   11   // Bound Import Directory in headers
define IMAGE_DIRECTORY_ENTRY_IAT            12   // Import Address Table
define IMAGE_DIRECTORY_ENTRY_DELAY_IMPORT   13   // Delay Load Import Descriptors
define IMAGE_DIRECTORY_ENTRY_COM_DESCRIPTOR 14   // COM Runtime descriptor
```

Dos *Data Directories* importanes son el de la posición 0 y 12, es decir **Export Directory** y **Import Address Table**. 
###### Export Directory
El *Export Directory* de un archivo de formato PE es una estructura de datos que contiene información sobre funciones y variables exportadas desde el ejecutable. Contiene direcciones de las funciones y variables exportadas, las cuales puede ser usadas por otros archivos ejecutables para acceder a las funciones o datos.
El *Export Directory* es generalmente encontrado en DLLs que exportan funciones, por ejemplo *kernel32.dll* exportando *CreateFileA*.
###### Import Address Table
El *Import Address Table* es una estructura de datos que contiene información sobre direcciones o funciones importadas desde otro archivo ejecutable. Las direcciones son usadas para acceder a funciones y datos alojados en otros ejecutables, por ejemplo *Aplication.exe* importa *CreateFileA* desde *kernel32.dll*. 

----
#### Section Table (PE Sections)
Inmediatamente seguido al Optional Header esta la Section Table, es un array de Headers para cada sección en el archivo PE. Cada Header contiene información sobre la sección a la que hace referencia.

Estas secciones contienen código y datos usados para crear un archivo ejecutable. Cada sección recibe un nombre único y mayormente contiene el código del ejecutable, datos o información de recursos. No existe un número constante de secciones ya que un compilador puede agregar, remover o mergear secciones dependiendo de la configuración. Algunas secciones también pueden ser agregadas más tarde de manera manual, por lo tanto son dinamicas y el campo *IMAGE_FILE_HEADER.NumberOfSections* ayuda a determinar la cantidad de secciones que existen.

Algunas de las secciones habituales más importantes que existe en la mayoría de arhicvos PE son:

- **.text**: Contiene el código del ejecutable, es decir, el código que fue escrito.
- **.data**: Contiene los datos inicializados, es decir, las variables inicializadas en el código.
- **.rdata**: Contiene únicamente la data *read-only*, es decir, las variables *constant* declaradas con el prefijo **const**. 
- **.idata**: Contiene las *Import Tables*. Estas son tablas de información relacionada a funciones llamadas durante el código. Esto es usado por el cargador de Windows (*PE Windows Loader*) que determina que DLL's serán cargadas al proceso, así como que funciones comenzaran a ser usadas de cada DLL. 
- **.reloc**: Contiene información sobre cómo arreglar las direcciones de memoria para que los programas puedan cargarse en la memoria sin errores.
- **.rsrc**: Usado para restaurar recursos como iconos y bitmaps.

IMAGE de cada Header Section
```C
typedef struct _IMAGE_SECTION_HEADER { 
0x00 BYTE Name[IMAGE_SIZEOF_SHORT_NAME]; 
	union { 
0x08 DWORD PhysicalAddress; 
0x08 DWORD VirtualSize; 
	} Misc; 
0x0c DWORD VirtualAddress; 
0x10 DWORD SizeOfRawData; 
0x14 DWORD PointerToRawData; 
0x18 DWORD PointerToRelocations;
0x1c DWORD PointerToLinenumbers;
0x20 WORD NumberOfRelocations; 
0x22 WORD NumberOfLinenumbers; 
0x24 DWORD Characteristics; 
};
```

Algunos de los elementos más importantes son

- **Name**: El nombre de la sección, por ejemplo *.text*, *.data*, etc.
- **PhysicalAddress** o **VirtualSize**: El tamaño de la sección cuando esta en memoria.
- **VirtualAddress**: Offset de donde empieza la sección en memoria. 

------
# Referencias

[^1]: **Dynamic Linker/Enlazador Dinámico**: Parte esencial del sistema operativo que se encarga de resolver y cinvular referencias a DLL en tiempo de ejecución cuando un porgrma se carga en memoria.
[^2]: **DOS**: Término utilizado para referirse a *Disk Operative System*, sistema operativo que se utiliza para gestionar y controlar el acceso a dispositivos de almacenamiento, como discos duros, unidades de disquete y unidades de CD/DVD en un equipo. Dos sistemas operativos conocidos con el nombre DOS son *MS-DOS* y *PC-DOS*. 
[^3]: **IMAGE**: En el contexto de arhcivos PE, IMAGE se utiliza en las estructuras de datos y encabezados en archivos PE para indicar que están relacionados con la implementación interna del formato PE y son parte del formato de archivo.
