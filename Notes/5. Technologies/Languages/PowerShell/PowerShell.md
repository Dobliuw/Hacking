# PowerShell 

En **PowerShell** *no hace falta* utilizar `return` para devolver un resultado. Cauqluier expresión cuyo resultado no sea capturado ni redirigido *se envía implícitamente al success output stream* (La salida de una función por ejemplo). Esto incluye un `New-Object`, un literal (`42`), el resultado de un cmdlet, etc. 

Ahora bien, entonces cuando o para que podríamos utilizar el `return` en **PowerShell**:

1. *Cortar la ejecución* del bloque/función de inmediato (*early-exit*).
2. (Opcionalmente) *emitir* un valor y cortar.