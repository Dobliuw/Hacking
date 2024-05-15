# Microsoft Terminal Services Client 

`mstsc` también conocido como *Microsoft Terminal Services Client*, tambie´n conocido como *RDC* (*Remote Desktop Connection*), es una herramienta proporcionada por Microsoft que permite a los usuarios realizar conexiones remotas a otros hostsa a través de conexiones de red.

- **Conexión de Escritorio Remoto**: `MSTSC` permite a los usuarios acceder al escritorio de una computadora remotamente como si estuviera sentado frente a ella. Esto puede ser útil para soporte técnico remoto, acceder a archivos y aplicaciones almacenados en otra computadora o administrar servidores y workstations de forma remota.
- **Acceso remoto seguro** `MSTSC` admite varias funciones de seguridad, incluidos protocolos de cifrado y autenticación, para garantizar conexiones remotas seguras. Es importante configurar correctamente los ajustes del escritorio remoto y utilizar contraseñas seguras par evitar el acceso no autorizado a sistemas remotos.

Para hacer uso de `MSTSC`, normalmente necesitaremos la sigueinte información:

- **Configuraciones de Firewall**: Permitir las conneciones de escritorio remoto, por defecto hace uso de 3389 TCP.
- **Dirección IP o hostname**: La dirección de red del equipo al que nos deseamos conectar.
- **Username and Password**: Credenciales necesarias para inciiar sesión en el equipo remoto.
- **Conectividad a Internet**: Tanto el equipo local como el reomoto deben estar conectadas a la misma red o ser accesibles a través de Internet.
- **Servicio Remote Desktop**: Será necesario tener habilitado en el equipo al que nos queremos conectar de manera remota el servicio de Remote Desktop o Terminal Service.

```powershell
# Enable Remote Desktop
> Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -Name "fDenyTSConnections" -Value 0

# Allow Remote Desktop through the firewall
> Enable-NetFirewallRule -DisplayGroup "Remote Desktop"

# Restart the Remote Desktop Services to apply changes
> Restart-Service TermService -Force
```

Conociendo el uso y sintaxis del comando `mstsc`:

```powershell
# Display help panel
> mstsc /?
```

Panel de ayuda:

![[mstsc_help_panel.png]]

Conexiones remotas haciendo uso de Remote Desktop:

```powershell
# Basic connection
> mstsc /v:{server[:port]}
# Connection giving credentials
> mstsc /v:{server[:port]} /u:{username} /p:{password}
# Launch full screen mode
> mstsc /v:{server[:port]} /f
# Connect to admin session
> mstsc /v:{server[:port]} /admin
# Setting custom resolution
> mstsc /v:{server[:port]} /w:{width} /h:{height} 
# Explore remote desktop connection settings
> mstsc /l 
# Import Remote Desltop connection settings
> mstsc /f:{file_path}
```