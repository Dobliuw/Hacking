# Microsoft Installer

*Microsoft Installer*, generalmente abreviado como *MSI*, es un componente del sistema operativo Windows que facilita la instalación, mantenimiento y eliminación de aplicaciones de software basada en computadoras Windows.
###### Purpose

- **Estandarizar la instalación**: MSI provee un formato de estandarización para la instalación de paquetes de software. Los desarrolladores utilizan archivos MSI para encapsular todos los archivos necesarios, recursos e instrucciones necesarias para instalar la aplicación.
- **Comportamiento de instalación coherente**: Los paquetes MSI garantizan un comportamiento de instalación coherente en diferentes sistemas Windows. Admiten funciones como instalaciiones silenciosas, reparaciones y desinstalaciones, haciendo que el despliegue del software sea más confiable y predecible.
- **Integración con *Windows Installer Service***: El servicio Windows Installer (`msiexec.exe`) interpreta y ejecutá paquetes MSI. Gestiona el procesos de instalación, incluyendo la extracción de archivos, el registro de componentes y la funcionalidad de reversión en caso de fallas en la instalación. 

Esta herramienta es una funcionalidad muy poderosa y clave cuando hablamos de la administración y manejo del sistema operativo, como profesionales de la ciberseguridad en el apartado de pentesting, esta herramienta puede ser de vital interes en caso de contar con determinados permisos en el sistema como podría ser *AlwaysInstallElevated*, privilegio que le otorga a los usuarios no administradores la capacidad de llevar a cabo la instalación de software usando permisos a nivel de sistema, lo que lo vuelve una vía de escalar privilegios.

---
# MSIEXEC.EXE

`msiexec.exe` es una utilidad de línea de comandos utilizada en Windows para instalar, modificar o eliminar paquetes *.msi*. 

```powershell
# Display the Windows Installer usage with Install, Logging, Display and more options
> msiexec.exe /?
```

Tras la ejecución del comando para solicitar el panel de ayuda de esta herramienta, se nos abrira una ventana en la cual podremos ver la sintaxis del comando, ejemplos de uso, explicación de los distintos tipos de opciones, etc.

![[windows_installer_help_guide.png]]

Podríamos llevar a cabo una simple instalación de un paquete *.msi* con el siguiente comando: 

```powershell
# Install a msi package without user interactio and with status messages
> msiexec.exe /i "X:\Path\to\our\installer.msi" /quiet
```

Podríamos modificar un paquete *.msi* previamente instalado, esto quiere decir que podríamos querer parchearlo, actualizarlo o reparar el mismo, por ejemplo, siempre haciendo uso del panel de ayuda podríamos repararlo:

![[repair_option_sectio_windows_installer.png]]

```powershell
# Modiying (Which could mean repari, update or patche existing installation)
> msiexec.exe /fa "X:\Path\to\our\repair.msi" /qn
```


