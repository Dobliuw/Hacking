# Post-Explotation

La **Post Explotación** comienza inmediatamente después de haber obtenido acceso inicial a un activo (Workstation, servidor, endpoint, aplicación, contenedor, etc.). Es esta fase, el foco ya no está en la vulnerabilidad que permitió el acceso, sino en el *control*, la *escalada*, el *lateral movement*, la *exfiltración de datos*, la *explotación interna* y cualquier deseo que tengamos a realizar comandados por los intereses propios o del cliente.

Como parte de un red team, se busca *entender el contexot del sistema comprometido* (Qué es, a quién pertenece, qué permisos tiene, qué conexiones mantiene) y moverse lateralmente con el menor ruido posible.

---
# Main targets

Los principales objetivos en el escenario ideal una vez ganado acceso sería:

1. **Stabilization & Persistence**.
	- Primer paso con el fin de evitar perder el acceso ganado.
	- Se busca establecer un canal estable y resiliente (Ej: C2, Reverse Shell Persistente, Backdoor, Beacon).
	- Ejemplo: Rgistrar un servicio en Windows con un binario firmado, usar `shtasks`, `WMI event subscriptions` o técnicas fileless con PowerShell/CLR.
2. **Privilege Scalation**.
	- Elevar permisos para obtener control administrativo o SYSTEM/root.
	- Se analizan *tokens*, *credenciales*, *configuraciones inseguras*, *binarios vulnerables*, *ACLs* y *servicios*.
	- Ejemplo: usar `PrintSpoofer`, enueración con `BloodHound`, `JuicyPotatoNG`, `LPE exploits` o abusar de configuraciones sudoers.
3. **Collection fo credentials**.
	- Extraer secretos en reposo o en memoria.
	- Ejempo: `mimikatz`, `lsass dump`, `secretsdump.py`, [[Pass The Hash]],`pass-the-ticket`, [[Kerberoasting Attack]], `dpapi` o volcados de *SAM* y *NTDS.dit* (Ej. [[Abuso de SeBackupPrivilege]]).
4. **Internal Reconnaissance** (Situational Awareness).
	- Descubrir usuarios, hosts, dominios, políticas de seguridad, segmentación de red y roles críticos.
	- Ejemplo: usar `net view`, `BloddHound`, `ldapsearch`, `SharpHound`, `ADRecon` o `Seatbelt`. 
5. **Lateral Movement**.
	- Usar credenciales o tokens válidos para privotar a otros sistemas.
	- Técnicas: `SMB exec`, `WinRM`, `WMI`, `RDP`, `PsExec`, `pass-the-ticket`o túneles (SSH, SOCKS, Chisel, Meterpreter Pivot, Socat).
6. **Advanced Persistence & Evasion**.
	- Instalación de backdoors o agentes discretos que sobrevivan reinicios y detección. 
	- Ejempo: `implant fileless`,  `registry run keys`, `scheduled tasks`,  `domain persistence` ([[Golden Ticket Attack]], Skeleton Key).
7. **Access to Critical Assets**.
	- Una vez controlado el entorno, el operador busca *objetivos de valor*: controladores de dominio, servidores de correo, bases de datos, repositorios de código, servidores CI/CD, backups, etc.
8. **Exfiltrations & Impact Demostration**.
	- Simular el robo de información sensible o la manipulación de recursos críticos.
	- En ejercicios reales se limita la extracción a *samples controlados* y se documento el posible impacto (Por ejemplo, "acceso a nóminas de emplados" sin robarlas).

----
# Workgroup vs Dominio

Cuando entramos a la *máquina local* (**Workstation**), nuestro usuario "vive en la SAM local" y el que nos autentica es el *propio equipo*. Cuando entramos al *dominio* (**Active Directory**), nuestra identidad viven en el AD y nos autentica el *Domain Controller*. 

1. Base local del equipo (**SAM local** de *\\\\W-DESKTOP*).
2. El Directorio Activo (AD) del dominio (Controladores de dominio - **DC**).

¿Que cambia? Bueno... mucho. Cambia el tipo de token que se recibe, los grupos que acompañan, los protocolos disponibles para utilizar y el alcance real en la red.

1. **Autentication**
	- *Local*: El `%LOGONSERVER%` es el hostname local, el token contiene grupos `BUILTIN\` y `EQUIPO\` y no hay *TGT Kerberos* del dominio.
	- *Dominio*: El `%LOGONSERVER%` es un *DC*, el token incluye `DOMAIN\DomainUsers` (Y otros), y `klist` muestra *TGT krbtgt/DOMAIN*. Esto habilita SSO Kerberos contra servicios con SPN (CIFS/HTTP/MSSQL/LADP.....).
2. **Rights Scope**
	- *Local*: Los privilegios terminan en dicho host. Podemos ser adminitradores locales y aun así no tener ningún derecho en el resto.
	- *Dominio*: Los grupos de dominio pueden otorgarnos accesos a recursos compartidos, servidores, apps, GPOs (Entre otras) o hasta de toda la organización.
3. **Policy Implementation**
	- *Local*: Recibimos solo *GPO Locales* (Si existen) y las configuraciones del propio equipo.
	- *Domain*: Se aplican *GPO de AD* por sitio/OU/usuario/equpo; eso dfine desde hardware hasta software permitido y scripts de logon.
4. **Autentication Protocol**
	- *Local*: Priman *credenciales locales* y accesos NTLM ad-hoc; sin TGT casi todo "SSO" de AD está fuera de alcance.
	- *Domain*: *Kerberos* es la norma, podemos solicitar TGSs a servicios del dominio y realizar ataques como [[Pass The Hash]], delegación, etc.
5. **Visibility & Enumeration**
	- *Local*: `Import-Module ActiveDirectory` suele fallar (No RSAT / sin permisos ni conectividad LDAP adecuada). Enumerar AD es limitado salvo que se conozcan credenciales de dominio explícitas.
	- *Domain*: Con un usuario estándar ya podríamos consultar LDAP, listar SPNs, OUs, GPOs, trusts, etc, de forma "silenciosa".
6. **Management & Auditing**
	- *Local*: La cuenta la administra cada equpo; contraseñas, bloqueo, expiración y adutorís se encuentran aisladas.
	- *Domain*: La cuenta es centralizada; políticas de contraseña, MFA, expiración, bloqueo y auditoría las define el AD para todo el entorno.

Distinguir si estamos en un cuenta de dominio  o en una cuenta de un equipo local:

```powershell
echo $env:USERDNSDOMAIN
```

- Output *vacío* da indicios de una cuenta *local*.
- Output como *dobliuw.example.local* indica sesión de cuenta de *dominio*.

```powershell
echo $env:LOGONSERVER
```

- Output *\\\\DOBLIUW* indica que es el propio host (Cuenta *local*).
- Output como *\\\\DC01* indica sesión de cuenta de *dominio*.

```powershell
klist
```

- Output *Cached Tickets: (0)* indica sesión de cuenta *local*.
- Output como *TGT krbtgt/DOBLIUW.EXAMPLE.LOCAL* indica sesión de cuenta de *dominio*

```powershell
whoami /all
systeminfo | findstr /i "Domain"
wmic computersystem get Domain,DomainRole
```

> [!warning] Local account still belong to AD
> Un **equpo puede estar unido a un dominio** y, aun así, podemos estar logueados como **usuario local**. En ese caso `wmic computersystem get Domain,DomainRole` nos arrojará *3* / *4* / *5* (*Miembro* / *Servidor* / *DC*), pero nuestra sesión no será de dominio. Si quisieramos loguearnos sin cerrar por ejemplo un RDP, abririamos una consola con credenciales de dominio:
> 
> ```powershell
> runas /netonly /user:DOMAIN\user powershell
> ```
> 
> Es **IMPORTANTE** entender que este comando *no autentica contra el DC* (Lo que indica que no se validan la password al momento de ingresarla) ni crea una sesión de dominio. Lo que hace es abrir un nuevo proceso (En este caso una *PowerShell*) con **dos capas distintas de indentidad**.
> 
> 1. **Local Token** (**Interactive**): Es el que define quien somos *en el equipo*. Este sigue siendo el usuario local (O el que se utilizo por ejemplo para abrir un RDP). Ese token no contiene grupos de dominio, no cambia la variable `%USERDNSDOMAIN%`, mismo `whoami /all`no muestra pertenencias de dominio y los permisos sobre el *filesystem local*, *servicios*, *registro*, etc., **son los del usuario local**. 
> 2. **Network Credentials** (**Impersonation for outbound**): Las credenciales de red ingresadas a la hora de ejecutar dicho comando quedan "adheridas" a ese proceso y a los hijos que herden el token. cada vez que **ese proceso** intenta *autenticarse contra un recurso remoto* (SMB / LDAP / HTTP / WinRM.....), Windows usa *esas credenciales* de **DOMAIN\User** para la negociación de seguridad. Ahí *recién* se autentica contra el DC si hace falta (Kerberos) o se negocia NTLM, y recién ahí podían aparecer tickets con el comando `klist`.

----
# Practical moment

```powershell

# I am in an AD? 
whoami /all 
echo %USERDNSDOMAIN%
echo %LOGONSERVER%

# Get WIndows version
Get-ComputerInfo | Select-Object WindowsProductName, WindowsVersion, OsHardwareAbstractionLayer
(Get-CimInstance Win32_OperatingSystem).Version
systeminfo

# List vaialable modules
Get-Module -ListAvailable
echo $env:PSModulePath 

# AD Infomration
Import-Module ActiveDirectory

# List DC
nltest /dsgetdc:DOMAIN.EXAMPLE.COM

ifconfig /all
arp -a

net share
net sessions


```