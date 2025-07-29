# Dual Boot 

Una **Dual Boot** o **Arranque Dual** es una configuración que permite tener dos o más sistemas operativos instalados en un mismo equipo físico, compartiendo hardware pero funcionando de manera completamente independiente. al encender el ssitema, un menú de araque permite al usuario elegir que sistema operativo iniciar.

Esto habilitar el uso de distintos entornos nativos, por ejemplo, un [Arch Linux](https://archlinux.org) basado en *Linux* ([[0. Linux Basics]]) y un *Windows* ([[0. Windows Basics]]), sin necesidad de virtualización ni hardware adicional. Es ideal para quienes requieren herramientas exclusivas de cada sistema operativo, o para prácticas de seguridad ,desarrollo o testing de sistemas.

----
# How **Bootloader** works in Dual Boot

El componente central de un  entorno *Dual Boot* es el conocido **Bootloader**, que en sistemas Linux es típicamente **GRUB** (**Gran Unifiend Bootloader**). GRUB se instala en la partición de arranque (O en la *ESP* - *EFI System Partition*, en setups *UEFI*) y tiene como misión presentar al usuario un menú con las distintas opciones de inicio disponibles.

El flujo básico de esto es:

1. El firmware *UEFI* detecta y ejecuta el loader registrado en la paritición `EFI`. 
2. Esta partición contiene entradas configuradas como:
	- `EFI\Microsoft\Boot\bootmgfw.efi` (Bootloader de Windows).
	- `EFI\GRUB\grubx64.efi`(GRUB, si se instaló Linux por ejemplo).
3. Si **GRUB** es loader prioritario, mostrará un menú como:

- [ ] ![[Pasted image 20250512211747.png|1000]]


> [!warning] Windows no detecta a Linux
> El *Windows Bootloader* tiende a sobreescribe cualquier bootloader presente (Como **GRUB**) al reinstalar o actualizar el sistema, especialmente si se reinstala desde medios de recuperación. Por eso es común tener que reinstalar GRUB luego de una instalación de Windows. Por el contrario **GRUB** esta diseñado para detectar múltiples sistemas operativos (Gracias a herramientas como `os-prober` ) y para sufrir una personalización y configuración a gusto (Gracias a herramientas como `grub-mkconfig`) además de ofrecer un menú de arranque flexible y extensible.


----
# Partitioning the Disks

Una correcta estructura de particiones es fundamental para un *Dual Boot* estable y mantenible. Las decisiones de particionado deben considerar:

- Que sistemas se van a instalar.
- Cantidad y tipo de discos disponibles (*HDD*/*SSD*/*NVMe*).
- Uso compartido de datos entre sistemas.
- Cifrado de particiones (Ej. *LUKS* en Linux, *BitLocker* en Windows).

 Ejemplo de setup clásico con discos separados: 

- Disco 1 (NVMe SSD):
	- `/dev/nvme0n1p1`: `EFI System Partition`(ESP)\[~300MB ].
	- `/dev/nvme0n1p2`: `C:`(Windows NTFS).
- Disco 2 (HDD o SSD secundario):
	- `/dev/sda1`: `/boot`o `/efi`. 
	- `/dev/sda2`: `/`(Root Linux, puede estar cifrado con *LUKS*).
	- `/dev/sda3`: `/home`(Opcional).
	- `/dev/sda4`: Partición compartida con Windows (NTFS) (Opcional).

> [!important] Recordatorio
> También es posible instalar ambos sistemas en un solo disco con particiones separadas virtuales, pero requiere mayor cuidado al instalar *GRUB* y conservar la *ESP* intacta.

> [!done]  Consideraciones de seguridad
> - Si Linux utiliza **cifrado con LUKS**, el *initramfs* deberá incluir hooks como `encrypt`y `keyboard`(Ver `/etc/mkinitcpio.conf`).
> - **BitLocker** puede romper el arranque si detecta cmabios en la partición EFI o en el orden de boot (Recomendado desactivar en setups dual boot).
> - El **Secure boot** de UEFI puede interferir con GRUB si no está correctamente firmado o si no se usan claves personalizadas (O se desactiva completamente).

> [!summary] Recomendaciones técnicas
> - Instalar *primer Windows*, luego cualquier distro basada en Linux.
> - Usar el modo **UEFI** en ambos sistemas (Evitar mezclar **BIOS**/**UEFI**).
> - Hacer backup del `ESP`(`EFI System Partition`) y la configuración de GRUB post instalación.
> - Regenerar GRUB con `grub-mkconfig -o /boot/grub/grub.cfg`y usar `os-prober`para detectar Windows.
> - Validar el orden de booteo con `efibootmgr`. 



