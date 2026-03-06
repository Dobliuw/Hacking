# WireGuard

[WireGuard](https://www.wireguard.com/#simple-network-interface) es un *tunel VPN* seguro, rapido y moderno. Esta orientado a ser simple y rápida, por lo que hace que realmente pentesters y red teamers la utilizen / configuren cuando montan su propia infraestructura.

Esta desición suele tener uqe ver más con operacionalidad, superficie de atauqe , simplicidad criptográfica y facilidad de automatización que con la privacidad.

Es importante enetnder que en el contexto de Hackers, montar un servidor VPN no suele tener que ver únicamente con el anonimato al navegar por internet, si no que se suelen buscar otros objetivos adicionales como:

- Pivoting entre infraestructuras.
- Egress controlado.
- Segmentar C2.
- Encapsular tráfico ofensivo.
- Acceso persistente a infraestructura.
- Red privada entre múltiples VPS.
- Ocultar dirección IP original de máquina/servidor atacante.

Por esto, **WireGuard** se volvío extremadamente popular, ya que tiene aproximadamente *~4k líneas de código en kernel*, volviendolo sumamente liviano en comparación de alguno de sus competidores, así mismo funciona en kernel y su configuración es sumamente sencilla.

- Ejemplo de configuración típico:

```conf
[Interface]
PrivateKey = {SERVER_PRIVATE_KEY}
ListenPort = 51820

[Peer]
PublicKey = {CLIENT_PUBLIC_KEY}
AllowedIPs = 10.10.0.2/32
```

Sin necesidad de certificados, TLS o PKI compleja, solo claves Curve25519.

-----
# Key Generation

WireGuard requiere *claves públicas* y *privadas* encodeadas en base64, por lo que podemos hacer uso de `wg` ([Habiendo instalado WireGuard](https://www.wireguard.com/install/)) para llevar a cabo esta tarea:

- Private.
```bash
umask 077
wg genkey > privatekey
```

- Public
```bash
wg pubkey < privatekey > publickey
```

-----
# Server and Client configuration

Por mi parte, lo primero que prefiero hacer es llevara cabo la configuración del **servidor**, por lo que comenzaremos con:

- Crear una nueva interfaz:
```bash
ip link add dev wg0 type wireguard
```

- Agregar un rango de red a utilizar por el server:
```bash
ip addresss add dev wg0 10.10.0.1/24
```

> [!tip] Only TWO peers
> En este caso el comando que nos interesa es:
> ```bash
> ip address add dev wg0 10.10.0.1 peer 10.10.0.2
> ```

- Utilizando un archivo de configuración como el de arriba mencionado, podríamos (Luego de setear *el rango de red*) configurar los peers:

```bash
wg setconf wg0 server.conf
```

- La interfaz tiene que ser dada de alta:

```bash
ip link set up dev wg0
```

> [!warning] Aditional
> Si queremos utilizar la vpn con salida a internet, deberemos utilizar `iptables` tanto en el lado del **cliente** como del **servidor** para aceptar o redirigir el tráfico según corresponda. En caso del servidor deberemos configurar que acepte cualquier tráfico entrante por *UDP* (Utilizado por WireGuard) en el puerto que hayamos configurado:
> 
> ```bash
> iptables -A INPUT -p udp --dport 7878 -j ACCEPT
> ```
> 
> Habilitar forwarding y permitirlo:
> ```bash
> sysctl -w net.ipv4.ip_forward=1
> iptables -A FORWARD -i wg0 -j ACCEPT
> iptables -A FORWARD -o wg0 -j ACCEPT
> ```
> 
> NAT hacia internet:
> ```bash
iptables -t nat -A POSTROUTING -s 10.10.0.0/24 -o eth0 -j MASQUERADE
> ```


De cara al **cliente** los pasos son los mismos, con la salvedad del archivo de configuración que se verá algo tal que así:

```conf
[Interface]
PrivateKey = {PRIVATE_SERVER_KEY}

[Peer]
PublicKey = {PUBLIC_CLIENT_KEY}
Endpoint = {VPS_IP}:7878
AllowedIPs = 10.10.0.0/24
PersistentKeepalive = 25
```

> [!warning] Aditional
> Como mencionamos, en el caso de que querramos disponer de utilizar la VPN con salida a internet, deberemos configurar rutas con excepción para no romper el acceso al host . (Tarea que realiza el script *wg-quick* automáticamente).
> 
> ```bash
> ip route add default dev wg0
> ip route add {VPS_IP} via 192.168.1.1 dev enp4s0
> ```
> 
> Adicionalmente, habría que retocar el archivo de configuración cambiando *AllowedIPs = 0.0.0.0/0* así como el `/etc/resolv.conf` (En caso de que tenga una IP de proveedor de servicio de internet) modificando a *nameserver 8.8.8.8*.



