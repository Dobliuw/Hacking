# Dual Boot 

Un **Dual Boot** o **Arranque Dual** es una configuración que permite tener dos o más sistemas operativos instalados en un mismo equipo, pero de forma independiente. Al encender el dispositivo, un menú permitirá elegir cuál de los sistemas operativos se quieren iniciar. Esto significa que se puede trabajar con diferentes sistemas operativos nativos (Por ejemplo un [Arch Linux](https://archlinux.org/) basado en *Linux* ([[0. Linux Basics]]) y un *Windows* ([[0. Windows Basics]])) sin necesidad de tener máquinas virtuales o de usar dispositivos diferentes.

----
# How **GRUB** works in Dual Boot

El **GRUB** (**Grand Unified Bootloader** - [[Operative Systems Basics#GRUB (Grand Unified Bootloader)]]) es el gesto de arranque que carga Linux o, si es configurado correctamente, también podría arrancar un sistema operativo Windows en caso de querer llevar a cabo un *Dual Boot* con este sistema operativo.

El flujo básico de esto es:

1. *BIOS* / *UEFI* arranca el disco con la paritición `EFI`. 
2. En esa partición hay un loader como **GRUB**.
3. **GRUB** te muestra un menú con las opciones, ejemplo:
	- Arch Linux
	- Windows Boot Manager

Es importante entender que Windows no ve a Linux, pero Linux, es decir el **GRUB** sí puede ver y arrancar Windows.

Esto se da por el *comportamiento del Window's Bootloader*, el cual generalmente tiende a sobreescribir los bootloaders existentes incluyendo el de cualquier otro sistema operativo, mientras que **GRUB**, el bootloader de Linux esta diseñado para detectar otros sistemas operativos y proveer un menú de inicio para determinar cual se quiere iniciar.