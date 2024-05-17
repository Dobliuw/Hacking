----
- Tags: #comandos #basico #redes
---
# Conexión a WiFi desde la terminal 

```shell
# Listar estado de las interfazes de red
nmcli dev status 
# Verificar estado de una determinada interfaz de red
nmcli radio wifi 
# Habilitar Wi-Fi
nmcli radio wifi on
# Buscar redes Wi-Fi cercanas
nmcli dev wifi list
# Establecer conexión con red Wi-Fi
nmcli dev wifi connect {network-ssid}
# Con seguridad WEP o WPA indiicar contraseña
nmcli dev wifi connect {network-ssid} password "{network-passwd}"
# --ask para no tipear password en pantalla
``` 
# Administracion de conexciones

 ```bash
 # Listar conexiones guardadas
 nmcli con show
 #  Desconectarse da la conexión
 nmcli con down {ssid/uuid}
 # Para conectarse a otra red
 nmcli con up {ssid/uuid} 
```