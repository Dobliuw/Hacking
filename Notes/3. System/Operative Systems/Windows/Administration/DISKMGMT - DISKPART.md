# Disk Management

La gestión de particiones, discos y volumenes es un componente crítico en la administración del sistema y por ende, como punto de interes para nostros.

- **Manejo de almacenamiento**: La gestión de discos permite a los adminitradores adminisrtar unidades de disco y particiones en un sistema Windows. Esto inlcuye tareas como crear, eliminar, formatear y cambiar el tamaño de particiones. La gestión adecuada del disco es esencial para optimizar los recursos de almacenamiento y garantizar la integridad de los datos.
- **Rendimiento del sistema**: La gestión eficiente del disco puede afectar significaticamente el rendimiento del sistema. Con una correcta configuración de las particiones del disco y los vólumenes de almacenamiento, los administradores puede prevenir la fragmentación de disco, mejorar las velocidades de *read*/*write* y garantizar que los archivos críticos del sistema tengan el espacio adecuado.
- **Protección de datos**. 
- **Recuperación de incidentes**. 

----
# DISKMGMT.MSC

La extensión `msc` proviene de *Microsoft Management Console*, framework para alojar herramientas administrativas llamadas complementos. Cada complemento proporciona capacidades en varios aspectos del sistema, en este caso indica que tras la ejecución del comando `diskmgmt.msc` se nos habrirar la *GUI* para la gestión de discos.

![[gui_diskmgmt.msc-stdout.png]]

---
# DISKPART

Por otro lado, tenemos la implementación de herramientas para la gestion de disco a través de la línea de comandos con comandos como `diskpart`. 

```powershell
# Launch the Diskpart utility from a administrative powershell
> diskapart
```

Una vez lanzado el comando `diskpart` se nos abrira una nueva v

```powershell
# List all disk
list disk
# Select a disk for further operations
select disk {disk}
# List partitions fon the selected disk
list partition
# Create a new partition on the selected disk
create partition primary size={size}

# Select a disk for further operations
select partition {partition}
# Delete a partition from the selected disk
delete partition
# Format a partition with a specified file system
format fs=NTFS quick
# Extends teh size of teh selected partition
extend
# Reduces the size of the selected partition
shrik desired={partition}
```