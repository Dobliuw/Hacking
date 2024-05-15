# Windows Management Instrumentation Command-Line

`wmic` (**Windows management Instrumentation Command-line**) es una herramienta de línea de comandos poderosa para los administradores de sistemas Windows y, por ende, para los pentesters... Provee una interfaz de línea de ocmandos para la infraestructura WMI, permitiendo a los usuarios consultar información del sistema, realizar tareas administrativas y manejar componentes del sistema de manera remota. Algunos de los usos más importantes a destacar como pentesters es:

- **System Enumeration**: Los pentesters podemos hacer uso de `wmic` para obtener información detallada acerca del sistema comprometido y auditado, incluyendo especificaciones del hardware, softwares instalados, processo corriendo, cuentas de usuario y configuraciones de red. Esta información nos puede ayudar a entender el entorno auditado así como a identificar potenciales vulnerabilidades.
- [[RCE - (Remote Command Execution)]]: `wmic` puede ser aprovechado por los pentesters o ciberdelincuentes para la ejecución arbitraria de comandos o scripts en el sistema remoto. A través de la explotación de permisos mal configurados o vulnerabilidades, los atacantes podrían ejecutar código malicioso remotamente haciendo uso de comandos `wmic`.
- **Privilege Escalation**: Los comandos de `wmic` pueden ejecutarse con privilegios elevados, especialmente si se ejecutan en un contexto de un usuario adminitrador. Los pentesters o ciberdelincuentes podrían abusar de `wmic` para escalar privilegios en el sistema comprometido ejecutando comandos privilegiados o modifcando configuraciones críticas del sistema.
- **Lateral Movement**: `wmic` habilita a los pentesters y ciberdelincuentes la capacidad de llevar a cabo movimiento lateral dentro de la red a través de la ejecución de comandos o scripts. Explotando autenticaciones debiles o permisos mal configurados, los atacantes podrían pivotear ([[Pivoting]]) entre sistemas y expandir su *foothold*. 
- **Data collection**: Los pentesters y ciberdelincuentes también podrían hacer uso de esta herramienta para la colección de información sensible y crítica en el sistema vícitma, incluyendo datos sensibles, entradas de registro, event logs y ajustes de configuración.

```powershell
# Show posible information to consult
> wmic /?
> wmic os
> wmic cpu
> wmic bios
# And more options that we can consutl

# Get OS information
> wmic os get Caption, OSArchitecture, Version
# Get CPU information
> wmic cpu get Name, MaxClockSpeed, NumberOfCores
# Get BIOS information
> wmic bios get Manufacturer, SMBIOSBIOSVersion, ReleaseDate
# Get Memory information
> wmic memorychip get BankLabel, Capacity, Speed
# Get disk drive information
> wmic diskdrive get Model, Size, InterfaceType
# List installed software
> wmic product get Name, Version
# Get network adapter information
> wmic nicconfig get Caption, IPAddress, MACAdress
# Get user account information
> wmic useraccount get Name, FullName, Description
# Start a service
> wmic service where "name='{service_name}'" call startservice
# Stop a service
> wmic service where "name='{service_name}'" call stopservice
# Restart a service
> wmic service where "name='{service_name}'" call restarservice
# Enable a remote desktop
> wmic /namespace:\\root\CIMv2\TerminalServices PATH Win32_TerminalServiceSetting WHERE (__Class !="") CALL SetAllowTSConnections 1
# Disable a remote desktop
> wmic /namespace:\\root\CIMv2\TerminalServices PATH Win32_TerminalServiceSetting WHERE (__Class !="") CALL SetAllowTSConnections 0
# Querying running process
> wmic process list brief
> tasklist
# Termina a process
> wmic process where "name='notepad.exe'" delete
```

