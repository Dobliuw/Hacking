# Service Control Manager

El comando `sc` en Windows es utilizado para comunicarnos con el `Service Control Manager` y servicios. Nos permite crear, modificar, arrancar, detener y consultar servicios en un sistema de manera local o remota.

```powershell
# Querying service status
> sc query {service_name}
# Starting a service
> sc start {service_name}
# Create a service
> sc create "DobliuwSvc" binPath="C:\Path\to\exectuable.exe"
# Delete a service
> sc delete {service_name}
# Changig service configuration
> sc config {service_name} start=auto
# Querying service dependencies
> sc qc {service_name}
# Granting service permissions
> sc sdset {service_name} D:(A;;CCLCSWRPWPDTLOCRRC;;;SY)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCLCSWLOCRRC;;;IU)(A;;CCLCSWLOCRRC;;;SU)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;WD)
```
