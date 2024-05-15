# REG

El comando `reg` en Windows nos permite interactuar con el *Registro de Windows*, esté se encuentra mencionado y explicado en la sección de [[0. Windows Basics]]. 

```powershell
# Adding a registry key
> reg add HKCU\Software\DobliuwSoftwareExample
# Adding a registry key and value
> reg add HKCU\Software\DobliuwSoftwareExample /v name /t REG_SZ /d "Dobliuw"
# Deleting a registry key 
> reg delete HKCU\Software\DobliuwSoftwareExample
# Exporting a registry key to a file
> reg export HKCU\Software\DobliuwSoftwareExample C:\Users\dobliuw\Desktop\dobliuw_software_backup.reg
# Importing a registry file
> reg import C:\Users\dobliuw\Desktop\backups\softwareBackup.reg
# Querying a registry key value
> reg query HKCU\Software\DobliuwSoftwareExample /v name
# Querying all subkeys and values under a key
> reg query HKCU\Software\DobliuwSoftwareExample /s
# Querying all values under a key
> reg query HKCU\Software\DobliuwSoftwareExample /v *
# Setting the value of a registry key
> reg add HKCU\Software\DobliuwSoftwareExample /v name /t REG_DWORD /d 0
```