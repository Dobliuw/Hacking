# PsExec

**PsExec** es una herrmaienta administrativa de sistema versátil de Microsoft que se puede utilizar para acceder de forma remota a un host de destino. es parte de la suite de herramientes Sysinternalas, su propósito principal es ayudar a los administradores del sistema a realizar tareas de mantenimineto remoto y ejecutar comandos en el host de destino. Como interfaz de línea de comandos, PsExec solo requiere que proporcione la dirección de destino, los detalles del usuario y la contraseña para obtener acceso al host de destino

---
# Requerimientos y usos

La herramienta de línea de comandos **PsExec**, creada por *Sysinternals*, permite la interacción remota con otros sistemas (Movimiento lateral) sin necesidad de instalar (Descarga y ejecución) utilizando diferentes credenciales (Impersonalización).

- **LanmanServer en ejecución**: El servicio de *LanmanServer* necesita estar siendo ejecutado en el host de la víctima. *LanmanServer* es responsable de la transmición de archivos e impresoras a traves de la red.

```powershell
# Attempt to start the LanmanServer service
> sc start LanmanServer
```

- **Puerto 445 TCP Accesible**: El puerto 445 TCP necesita ser accesible en el host víctima ya que este puerto es usado por *PsExec* para la comunicación a través de la red. Tiene que estar abierto y accesible para poder establecer una conexión, sin la posibilidad de acceder a este puerto, PsExec no va a poder llevar a cabo la comunicación con el sistema target.

- **Permisos avanzados en el sistema víctima**: Para ejecutar comandos de manera remota haciendo uso de PsExec, la cuenta de usuario utilizada para hacer uso de esta utilidad tiene que tener los suficientes permisos en el sistema remoto. Esto usualmente incluye privilegios administrativos o derechos de accesos apropiados para realizar esta acción deseada.

- **Modificación de clave de registro para UAC**: Como vimos en [[0. Windows Basics]], el *UAC* (*User Access Control*) es una caracteristica de seguridad de Windows que solicita credenciales o confirmación administrativa tras el intento de ejecución de un software que puede ser critico, en este caso, PsExec requiere que la clave de registro (*Registro de Windows* también explicado en [[0. Windows Basics]]) `LocalAccountTokenFilterPolicy`, en caso de estar en *0*, cambiarlo a *1* para que el UAC no filtre las conexiones administrativas remotas y bloquee a la par que solicite credenciales de administrador mediante una GUI.

```powershell
# Change the value LocalAccountTokenFilterPolicy of the spcified key:
> reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" /v LocalAccountTokenFilterPolicy /t REF_DWORD /d 1 /f
# /v {value_name} -> value to change/add 
# /t {value_type} -> value type
# /d {value} -> the value it self
# /f -> Force overwriting the existing registry entry without prompt.
# ---- THIS ALL OPTION COULD BE SEEING WITH "reg add /?" command ----- 

# VALUES TYPES
# REG_SZ / REG_MULTI_SZ / REG_EXPAND_SZ (Strings)
# REG_DWORD (Integer, 32-bit decimal number)
# REG_BINARY (Binary, hex value)
```

- **Personalización del nombre de Servicio**: PsExec permite la personalización del nombre de servicio haciendo uso de la flag `-r`. Esto puede ser muy útil para evadir detecciones o ocultar/disfrazar la prescencia de PsExec en el sistema víctima, el nombre por defecto de este servicio es `PsExecsvc`. 

```powershell
# Run a cmd instance in the remote system with the service "dobliuwsvc" insted PsExecsvc
> psexec -r dobliuwsvc \\{hostname} cmd.exe
```

Tener en cuenta que la ejecución de `psexec` será posible siempre y cuando estemos intentando acceder remotamente al sistema víctima desde un sistema Windows, en caso de hacer uso de sistemas operativos basados en Linux, podríamos hacer usos de herramientas como `impacket-psexec` provenientes de la *suite de impacket* u otras alternativas como:

- Metasploit psexec (`msf > use exploit/windows/smb/psexec`).
- Cobalt Strike (*Utiliza C$ y ADMIN$ para movimiento lateral*).
- Empire PsExec (*MITRE ATT&CK: T1035, T1077*).
- Cualquier framework de C&C, podríamos descargar el código y compilarlo con diferentes nombres para los valores, nombres de "pipes", etc.

Con *PsExec* podríamos:

- Crear cuentas en los equipos remotos (*T1136.002*).
- Modificar o crear procesos, podríamos escalar privilegios mediante la flag `-s` (Trasladarnos de Administrator a SYSTEM | *T1543.003*). 
- Utilizarlo como herramientas de transferencia de archivos lateral (*T1570*).
- Escribir programas en **ADMIN$** y ejecutar comandos en los sistemas remotos (*T1021.002*).

- Recursos: [Movimiento lateral con PsExec](https://www.mindpointgroup.com/blog/lateral-movement-with-psexec)