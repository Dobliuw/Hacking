# USB Rubber Ducky

El **USB Rubber Ducky** es un dispositivo que se presenta como una unidad USB, pero en realidad actúia como un teclado programable que puede enviar pulsaciones de teclas predefinidas a un equipo. Esto permite automatizar tareas y realizar ataques de inyección de comandos en cuestión de segundos.

----
# Using

---
# Mitigation

```powershell
> reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v ConsentPromptBehaviorAdmin /t REG_DWORD /d 1
```

