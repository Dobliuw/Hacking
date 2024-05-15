# Microsoft System Configuration Utility

`msconfig` o *Microsoft System Configuration Utility*, es una utilidad de los sistemas Windows que permite a los usuarios configurar varias opciones de inicio en el sistema así como diagnosticar problemas en la configuración del mismo. Proporcina una interfaz para administrar programas de inicio, servicios, configuración de inicio y otras configuraciones del sistema.

- **Configuración del Sistema**: Los usuaris pueden modificar el comportamiento de inicio, incluyendo habilitar o deshabilitar elementos de inicio, servicios y opciones de inicio.
- **Programas de Startup**: Los usuarios puede visualizar y manejar aquellos programas que inician automaticamente cuando el sistema se inicia. Esta característica permite a los uusarios controla cuales programas deberán seguir este comportamiento, mejorando potencialmente los tiempos de inicio y rendimiento del sistema.
- **Servicios**: Los usuarios pueden ver y manejar los servicios del sistema que corren en segundo plano. Esto incluye ejecutar, detener y deshabilitar servicios cuand sea necesario.
- **Configuración de inicio**: Los usuarios pueden modificar las configuraciones de boot, como el inicio en *Safe Mode* o cambiando la duración del *boot menu*.
- **Herramientas**: `msconfig` además ofrece acceso a herramientas adicionales del sistema, como puede ser *Event Viewer*, *System Information* y *Task Manager*, convirtiendolo en un eje central para troubleshooting y diagnostico del sistema.

```powershell
# Display the Microsoft System Configuration Utility window
> msconfig
```

![[msconfig_windows.png]]