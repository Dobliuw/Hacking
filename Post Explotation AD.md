		s# Post-Explotation

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

Bypass SSL/TLS secure chanel needed for `Invoke-WebRequest`: 

```powershell
add-type @"
    using System.Net;
    using System.Security.Cryptography.X509Certificates;
    public class TrustAllCertsPolicy : ICertificatePolicy {
        public bool CheckValidationResult(
            ServicePoint srvPoint, X509Certificate certificate,
            WebRequest request, int certificateProblem) {
            return true;
        }
    }
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy

[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Ssl3, [Net.SecurityProtocolType]::Tls, [Net.SecurityProtocolType]::Tls11, [Net.SecurityProtocolType]::Tls12
```

![[Pasted image 20251109214939.png]]

Expose port to internet 

```powershell
New-NetFirewallRule -DisplayName "HTTP-8888" `
  -Direction Inbound -Action Allow -Protocol TCP -LocalPort 8888

python3 -3 -m http.server {port} --bind 0.0.0.0 --directory C:\ruta\a\archivos

```

----
# Active Directoy Vocabulary (LDAP, DNS, etc.)

- **FQDN** (*DNS*): **Fully Qualified Domain Name**. Es un nombre DNS completo que identifica un host o un dominio en la jerarquí de DNS. 

Ejemplo: *dc01.dobliuw.local.com*

- **DN** (*LDAP* / *AD*): En un entorno de active directoy los objetos no se nombran con DNS si no con **DN** (**Distinguished Name**), una ruta jerárquica de atributos LDAP. Los fragmentos más comunes son:
	- **DC=**: *Domain Component*.
	- **OU=**: *Organizational Unit*.
	- **CN=**: *Common Name* (Usado para objetos genéricos: usuarios, grupos, equipos, contenedores) (CN=Users, CN=Computers, etc.).
	
Ejemplo de un objeto DN:

Usuario Owen Bonoris que trabaja en Ciberseguridad (`CN=Owen Bonoris,OU=Cybersecurity,DC=dobliuw,DC=local,DC=com`).

- **Base DN**: Objeto raíz (**defaultNamingContext**), es "la raíz" desde donde se busca ese dominio.

- **NC**: **Naming Context** es una paritición lógica del AD.

- **ADSI**: (**Active Directory Service Interfaces**) Es un conjunto de interfaces COM de WIndows que permiten a las aplicaciones acceder a los servicios de diretorio como LDAP.

- **RootDSE**: (**Directory Service Angent-Specific Entry**) es una entrada especial de solo lectura del servidor LDAP

---
# Enumerating AD from Domain account

Validar estar logueado en una cuenta de dominio:

```powershell
whoami /all
klist
echo $env:USERDNSDOMAIN
echo $env:LOGONSERVER
nltest /dsgetdc:$env:USERDNSDOMAIN
wmic computersystem get Domain,DomainRole
```

Obteniendo información de dominios de confianza y controladores de dominio en el AD:

```powershell
nltest /dclist:$env:USERDNSDOMAIN
nltest /domain_trusts
```

##### Enumerating LDAP DN Objects

Descubrir los naming contexts (**NC**) correctos desde *RootDSE*.

```powershell
$rootDse = [ADSI]("LDAP://RootDSE")
$defaultNC = $rootDse.defaultNamingContext  
$configNC = $rootDse.configurationNamingContext
```

Enlazar al objeto el dominio EXACTO y ver las propiedades del mismo.

```powershell
$domainEntry = [ADSI]("LDAP://$defaultNC")
$domainEntry.Properties | Format-List
```

Usar *DirectorySearcher* para apuntar explícitamente al **DN** y definir posteriormente criterios de búsqueda.

```powershell
$searcher = New-Object System.DirectoryServices.DirectorySearcher
$searcher.SearchRoot = $domainEntry
$searcher.SearchScope = [System.DirectoryServices.SearchScope]::Base # AD Root object

$searcher.Filter = "(objectClass=domainDNS)"
($searcher.FindOne()).Properties | Format-List
```

----

En **Active Directory** cada *servicio autenticable* se indentifica con un **SPN** (**Service Principal Name**) (Por ejemplo: `cifs/filtersrv01.example.local`). Los SPN viven como *atributos de cuenta* (Normalmente de *usuario de servicio*, a veces máquinas).

Como hemos visto en diagramos como [[KERBEROS_AUTHETICATION_FLOW]], el flujo normal es:

- **AS-REQ** / **AS-REP**: El cliente obtiene un TGT mediante KDC (`krbtgt\domain.example.local`).
- **TGS-REQ** / **TGS-REP**: Con el TGT se solicita un TGS para un SPN concreto.
- **AP-REQ** / **AP-REP**: Con el TGS se trata de autenticar contra el servicio.

Todo esto se puede visualizar con el comando `klist`, el cual *muestra tickets en caché* y *eventos en DC* si hay logging.

- [[Hashes NT, NTLM y NTLMv2]]: Si no hay Kerberos (No hay SPN, utilizamos IP, etc.) Windows opta por utilizar NTLM, Ahí el secret es el [[Hashes NT, NTLM y NTLMv2#Hash NT (NTLM Hash)]] y da lugar a técnicas como [[Pass The Hash]].

----
# Enumerating Users & SPNs

Tener un listado de *cuentas de usuario* con atributos que sean de interes:

- `adminCount=1`: La cuenta estuvo en *grupos protegidos* (Ejemplo: Domain Admins).
- `userAccountControl`: Trae bits clave, ejemplo:
	- `DONT_EXPIRE_PASSWORD=0x10000`.
	- `DONT_REQ_PREAUTH=0x400000`.
	- `SMARTCARD_REQUIRED=0x40000`.
- `lastLogonTimestamp`: Aunque es replicado y no exacto, es útil para ver la "antigüedad".
- `pwdLastSet`: Sugiere candidatos con credenciales sensibles o filtradas (Servicios antiguos con credenciales no rotadas).
###### Using AD Module
- Búscar SPNs utilizando modulo de AD.
```powershell
Import-Module ActiveDirectory
Get-ADServiceAccount -Filter 'ServicePrincipalNames -like "*"' | Select-Object -ExpandProperty ServicePrincipalNames
```

- Filtrar por Servicios especiales (Ejemplo *http*).
```powershell
Get-ADServiceAccount -Filter 'ServicePrincipalNames -like "*http*"' | Select-Object -ExpandProperty ServicePrincipalNames
```

###### Without using AD Module

```powershell
$rootDse = [ADSI]("LDAP://RootDSE")
$defaultNC = $rootDse.defaultNamingContext  
$configNC = $rootDse.configurationNamingContext
$searchRoot = [ADSI]("LDAP://$defaultNC")

$ds = New-Object System.DirectoryServices.DirectorySearcher
$ds.SearchRoot = $searchRoot
$ds.PageSize = 1000
$ds.ReferralChasing = [System.DirectoryServices.ReferralChasingOption]:All

# Only NORMAL USERS
$ds.Filter =  "(&(objectCaterogry=person)(objectClass=user))"

# Pentesting interest attributes
$props = @(
  "samaccountname","userprincipalname","distinguishedname",
  "memberof","whencreated","whenchanged","lastlogon","lastlogontimestamp",
  "pwdlastset","badpwdcount","admincount","useraccountcontrol"
)
$ds.PropertiesToLoad.Clear(); $null = $ds.PropertiesToLoad.AddRange($props)

$users = $ds.FindAll() | ForEach-Object {
  $p = $_.Properties
  # Helper para convertir timestamps (LDAP file time)
  function ToDate($v){ if($v){ [DateTime]::FromFileTime([Int64]$v[0]) } else { $null } }
  [pscustomobject]@{
    sAMAccountName = ($p["samaccountname"]      | Select-Object -First 1)
    UPN            = ($p["userprincipalname"]   | Select-Object -First 1)
    DN             = ($p["distinguishedname"]   | Select-Object -First 1)
    MemberOf       = (@($p["memberof"])         -join ";")
    WhenCreated    = ($p["whencreated"]         | Select-Object -First 1)
    WhenChanged    = ($p["whenchanged"]         | Select-Object -First 1)
    LastLogonTS    = ToDate  $p["lastlogontimestamp"]
    PwdLastSet     = ToDate  $p["pwdlastset"]
    BadPwdCount    = ($p["badpwdcount"]         | Select-Object -First 1)
    AdminCount     = ($p["admincount"]          | Select-Object -First 1)
    UAC            = ($p["useraccountcontrol"]  | Select-Object -First 1)
  }
}

# Guardalo para tus apuntes
$Out = "C:\Temp\adrecon"; New-Item -ItemType Directory -Force -Path $Out | Out-Null
$users | Export-Csv "$Out\users_basic.csv" -NoTypeInformation -Encoding UTF8
```


```powershell
# Todos los SPN del dominio (puede tardar; filtra por tipo si querés)
setspn -Q */* > "$Out\spn_all_setspn.txt"

# Ejemplos por servicio:
setspn -Q MSSQLSvc/*   > "$Out\spn_mssql.txt"
setspn -Q HTTP/*       > "$Out\spn_http.txt"
setspn -Q CIFS/*       > "$Out\spn_cifs.txt"
setspn -Q HOST/*       > "$Out\spn_host.txt"   # Ojo: muchísimos serán de cuentas de máquina

```

```powershell
$ds = New-Object System.DirectoryServices.DirectorySearcher
$ds.SearchRoot   = $SearchRoot
$ds.SearchScope  = "Subtree"
$ds.PageSize     = 1000
$ds.Filter       = "(&(objectClass=user)(servicePrincipalName=*))"  # SPN en cuentas de usuario
$ds.PropertiesToLoad.Clear()
$null = $ds.PropertiesToLoad.AddRange(@("samaccountname","userprincipalname","serviceprincipalname","useraccountcontrol","pwdlastset"))

$spnUsers = $ds.FindAll() | ForEach-Object {
  $p = $_.Properties
  function ToDate($v){ if($v){ [DateTime]::FromFileTime([Int64]$v[0]) } else { $null } }
  [pscustomobject]@{
    sAMAccountName = ($p["samaccountname"]      | Select-Object -First 1)
    UPN            = ($p["userprincipalname"]   | Select-Object -First 1)
    SPNs           = (@($p["serviceprincipalname"])) -join ";"
    UAC            = ($p["useraccountcontrol"]  | Select-Object -First 1)
    PwdLastSet     = ToDate $p["pwdlastset"]
  }
}

$spnUsers | Export-Csv "$Out\spn_users.csv" -NoTypeInformation -Encoding UTF8

```

TOP RISKS
```powershell
# Carga el CSV de usuarios con SPN
$SPN = Import-Csv "$Out\spn_users.csv"

# Helpers para detectar flags en UAC
function HasFlag($uac,[int]$flag){ if($uac -and $flag){$true}else{$false} }

$DONT_EXPIRE = 0x10000
$DONT_PREAUTH= 0x400000   # (esto último no es típico en service accounts, pero por si aparece)

# Ejemplos de "vistas" útiles para apuntes:
$SPN_SQL  = $SPN | Where-Object { $_.SPNs -match "MSSQLSvc/" }
$SPN_HTTP = $SPN | Where-Object { $_.SPNs -match "HTTP/" }
$SPN_CIFS = $SPN | Where-Object { $_.SPNs -match "cifs/" }

# Prioriza: contraseñas viejas o que "no expiran", adminCount, etc.
$TopRisks = $SPN | Where-Object {
  (HasFlag([int]$_.UAC,$DONT_EXPIRE)) -or
  ($_.PwdLastSet -and $_.PwdLastSet -lt (Get-Date).AddMonths(-12))
}
$TopRisks | Export-Csv "$Out\spn_users_prioritized.csv" -NoTypeInformation -Encoding UTF8

```

GET ASP-REQ CANDIDANTS

```powershell
$ds = New-Object System.DirectoryServices.DirectorySearcher
$ds.SearchRoot   = $SearchRoot
$ds.SearchScope  = "Subtree"
$ds.PageSize     = 1000

# UAC bit 0x400000 => DONT_REQ_PREAUTH
$ds.Filter       = "(&(objectClass=user)(userAccountControl:1.2.840.113556.1.4.803:=4194304))"
$ds.PropertiesToLoad.Clear()
$null = $ds.PropertiesToLoad.AddRange(@("samaccountname","userprincipalname","pwdlastset"))

$asrep = $ds.FindAll() | ForEach-Object {
  $p=$_.Properties
  function ToDate($v){ if($v){ [DateTime]::FromFileTime([Int64]$v[0]) } else { $null } }
  [pscustomobject]@{
    sAMAccountName = ($p["samaccountname"]|Select-Object -First 1)
    UPN            = ($p["userprincipalname"]|Select-Object -First 1)
    PwdLastSet     = ToDate $p["pwdlastset"]
  }
}
$asrep | Export-Csv "$Out\asrep_candidates.csv" -NoTypeInformation -Encoding UTF8

```

----
# PoweShell Tools

[PSTools](https://learn.microsoft.com/en-us/sysinternals/downloads/pstools)