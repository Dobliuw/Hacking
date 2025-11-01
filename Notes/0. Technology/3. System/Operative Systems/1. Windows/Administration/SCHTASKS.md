# Schedule tasks

Las tareas programadas son eventeos que han sido programadas para correr en cierto intervalo de tiempo, como puede ser una vez al día, una vez por ahora o una vez por semana. Estas tareas pueden ser utilizadas para automatizar múltiples actividaes. De cara a nosotros, así como de los ciberdelincuentes, esta funcionalidad es crucial por diversos motivos.

- **Persistence**: Los atacantes pueden establecer persistencia en un sistema comprometido y mantener acceso abusando de tareas programadas para ejecutar código malicioso en intervalos regulares, asegurando el acceso continuo al sistema incluso luego del ingreso al sistema inicial.
- **Payload Delivery**: Las tareas programadas pueden ser utilizadas para la entrega de *payloads* o ejecución de scripts maliciosos en el sistema. Creando una tarea programada para correr un payload específico en un determinado tiempo o evento que detone a esta, un atacante podría automatizar la ejecución de código malicioso.
- **Privilege Escalation**: También pueden ser utilizadas para aumentar nuestro privilegio, especialmente si esta configuradas para ejecutarse por medio de una cuenta privilegiada o de sistema. Explotando *misconfiguration scheduled tasks* podríamos ganar privilegios y comprometer potencialmente el sistema.
- **Data Exfiltration**: También podríamos hacer uso de estas para en intervalos regulares de tiempo seleccionables exfiltrar información sensible del sistema comprometido hacia el C&C. Programando tareas para transferir archivos o ejecutar comandos de red, los atacantes podrían extraer información confidencial.
- **Lateral Movement**: Las tareas programadas también pueden facilitarnos el trabajo de movernos lateralmente a otros equipos dentro de la red ejecutando comandos o scripts en sistemas remotos. Un atacante podría ganar acceso a un sistema, hacer uso de las tareas programadas para pivotear ([[Pivoting]]) a otro sistema y expandir su *foothold*. 
- **Evasion**: Los atacantes podrían utilizar estas tareas para evadir detecciones de herramientas de seguridad o antivirus. Al programar actividades maliciosas fuera del horario laboral o utilizar nombres de tareas que parezcan legítimas, los atacantes podrían pasar desapercibidos y evitar la detección por parte de las defensas automatizadas.

----
# SCHTASKS

El comando `schtasks` en Windows nos permite crear *schedule tasks* o *tareas programadas* para que se ejecuten en un momento específico. Nos permite crear, eliminar, consultar, cambiar, ejecutar y finalizar tareas programadas en un sistema local o remoto.

```powershell
# Display help panel
> schtasks /?
> schtasks /create /?
> schtasks /query /?
# ... We can display help panel for each option

# Create a new scheduled task
> schtasks /create /tn "DobliuwTask" /tr "C:\Path\To\The\Executable.exe" /sc daily /st 09:00
# Delete a scheduled task
> schtasks /delete /tn "DobliuwTask"
# Query scheduled task
> schtasks /query
# Run a scheduled task
> schtasks /run /tn "DobliuwTask"
# Change properties of a scheduled task
> schtasks /change /tn "DobliuwTask" /tr "C:\NewPath\To\The\Executable.exe" /sc weekly
# End a running scheduled task
> schtasks /end /tn "DobliuwTask"
# Export a scheduled task to XML
> schtasks /query /tn "DobliuwTask" /xml > DobliuwTaskExported.xml
# Import a scheduled task from XML
> schtasks /create /xml /DobliuwTask.xml /tn "DobliuwTask"
```