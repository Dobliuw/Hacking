# PsExec

- Cada ejecución de PsExec instala un nuevo servicio (Event ID 7045 creación de servicios con el nombre de psexecsvc en ejecución por defecto) y deja una copia del binario en el recurso administratvo *ADMIN$*, finalizada la ejecución se elimina.
- Revisar la comunicación entre procesos *Pipes* para indentificar la comunicación, existe 2 tipos de Pipes explicados en [[Named and Unnamed Pipes]]. 
- Revisar los *pipes* en busca de ejecución o clones clones \\\\.\\pipe\\DobliuwC2, para PSEXECSVC (\\\\.\\pipe\\psexecsvc)
- Validar la clave de registro, indica que fue ejecutado HKEY_CURRENT_USER\\Software\\Sysinternals\\psexec\\eulaacceptede\\psexecsvc
- Revisar el diario del sistema de archivos NTFS para obtener evidencia del proceso en ejecución (Copia del binario en recurso administrativo) o ejecutado.
- Reconocimiento del hash/nombre del proceso.
- Revisar nombre de procesos o servicios creados, asociados a otras detecciones sospechosas que tengan conexiones de red en puerto 445.
- Revisar evento de creación de archivo Event ID 11 (Escritura de psexecsvc.exe).
