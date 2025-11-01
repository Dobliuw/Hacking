# Group Policy 

La directiva de grupo es una característica de la familia de sistemas operativos Windows. Una *Directiva de Grupo* o *Group Policy*, es un conjutno de reglas que controlan el entorno de trabajo de cuentas de usuario y cuentas de equipo.

----
# GPEDIT.MSC

La herramienta `gpedit.msc` es una herramienta poderosa en Windows para manejar varios ajustes del sistema y configuraciones dentro de una organización relacionadas a las políticas de grupos.

```powershell
# Deploy the Local Group Policy Editor windows
> gpedit.msc
```

![[gpedit.msc_image.png]]

----
# GPMC, GPUpdate, GPResult

- **Group Policy Management Console** (**GPMC**): El comando `gpmc.msc` provee una interfaz gráfica para la administración de *Group Policy Objects* (*GPOs*) en entornos de Active Directory. Si bien no es una herramienta de línea de comandos, ofrece un control centralizado sobre las políticas através del dominio.

```powershell
# To open de Grop Policy Management Console
> gpmc.msc
```

- **GPUpdate**: La utilidad de línea de comandos `gpupdate` es utilizada para actualizar los ajustes de políticas de grupos en un host local o para un usuari esepecífico en un entorno de Active Directory. Ejecutando`gpupdate` sin ningún parametro, actualizamos las políticas del usuario y del host local.

```powershell
# Force an inmmediate update of group policy
> gpupdate /force
# Perfrom a background update without displaying progress messages
> gpupdate /force /quiet
```

- **GPResult**: Esta utilidad de línea de comandos muestra la *Resultant Set of Policy* (*RSOP*) para un usuario o un host. Muestra que configuración de política de grupo han sido aplicadas al usuario o al host local, incluidas las heredadas de los contenedores principales de Active Directory.

```powershell
# Display teh RSoP for teh current user and host
> gpresult /r
# Display the RSoP for a specific user and host
> gpresult /user {username} /scope {computer} /r
```