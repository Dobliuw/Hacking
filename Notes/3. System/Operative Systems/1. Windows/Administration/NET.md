# NET

El comando `net` en Windows proporciona una amplia gama de funcionalidades relacionadas con redes, cuentas de usuario, serivicos y más.

- **Manejo de cuentas de Usuario**: Haciendo uso de `net user` podemos gestionar y configurar cuentas de usuario, inlcuso crear, modificar y eliminar estas, cambiar contraseñas y gestionar membresías de grupos.

```powershell
# Display help panel
> net user /?
# Create a new user
> net user {username} {password} /add
# Delete a user
> net user {username} /delete
# Change user password
> net user {username} {new_password}
```

- **Configuración de red**: Comandos como `netsh` nos permiten gestionar mútiples configuraciones de red, como direcciones IP, interfaces, reglas de firewall y más.

```powershell
# Display help panel
> netsh /?
# View network interfaces
> netsh interface show interface
# Set a static IP address
> netsh interface ip set address "Local Area Connection" static 192.168.1.100 255.255.255.0
```

- **Gestión de servicios**: `net start`, `net stop` y `net pause` son comandos que nos permiten el control de Servicios en Windows desde CLI.

```powershell
# Start a service
> net start {servicename}
# Stop a service
> net stop {servicename}
# Pause a service
> net puase {servicename}
```

- **Compartir archivos**: Podríamos hacer uso de comandos como `net share` para poder llevar a cabo uso del protocolo SMB para crear, ver y eleminar recursos compartidos. A esto se hace mención en el apartado de *Transferencia de archivos* de [[0. Windows Basics]].

```powershell
# Visualize all shared folders
net share
# Visualize a specific shared folder
net share {share_name}
# Create shared folder with wide-open access
net share {share_name}={path} /GRANT:Everyone,FULL
# Delete a specific shared folder
net share {share_name} /DELETE
```

- **Diagnostico de red**: Comandos como `netstat` nos proveen información sobre conecciones de red, tablas de enrutamiento y interfazes de red.

```powershell
# Display all TCP Listening connecitons
> netstat -nat -p TCP | findstr /I listening
# -n -> Displays addresses and port numbers in numerical form.
# -a -> Displays all connections and listening ports.
# -t ->  Displays the current connection offload state.
# -q ->Shows connections for the protocol specified by proto; proto
# may be any of: TCP, UDP, TCPv6, or UDPv6.  If used with the -s
# option to display per-protocol statistics, proto may be any of:
# IP, IPv6, ICMP, ICMPv6, TCP, TCPv6, UDP, or UDPv6.
```

- **Usos varios**: Algunos usos que se le puede dar a `net` no fueron mencionados en el apartado de arriba, como podría ser la declaración de un nueva unidad para un disco vinculado a un recurso compartido o listar información de un dominio, entre otras.

```powershell
# Assign letter X to a new drive bound with a sharename
> net use X: \\server\share_folder
# List information about a specific domain
> net view /DOMAIN:{domain}
```