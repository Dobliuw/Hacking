# CLI Linux Connection

- Using **nmcli**
```shell
# List network status
nmcli dev status 
# Check network interface status
nmcli radio wifi 
# Enable Wi-FI
nmcli radio wifi on
# Search near SSIDs
nmcli dev wifi list
# Establish connection 
nmcli dev wifi connect {network-ssid}
# With WEP or WPA security insert pass
nmcli dev wifi connect {network-ssid} password "{network-passwd}"
# --ask to don't write pass into screen
``` 

- Using **iw**
```bash
# If iw daemon is not up
sudo systemctl enable iwd
sudo systemctl start iwd

# Enter to Interactive Shell
iwctl
# List Devices
device list
# Scan for Networks
station {interface} scan
# List Available Networks
station {interface} get-networks
# Connecto to a Network
station {interface} connect {SSID}
# Quit 
exit
```
# Administrting connections

 ```bash
 # List saved connections
 nmcli con show
 # Disconnect
 nmcli con down {ssid/uuid}
 # Connect to another savedqdeb connection
 nmcli con up {ssid/uuid} 
```