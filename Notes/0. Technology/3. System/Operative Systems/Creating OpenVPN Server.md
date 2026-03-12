```bash
sudo apt update
sudo apt install openvpn -y

cp /usr/share/doc/openvpn/examples/sample-config-files/server.conf /etc/openvpn/server/

sudo mkdir -p /etc/openvpn/easy-rsa
sudo cp -r /usr/share/easy-rsa/* /etc/openvpn/easy-rsa/
sudo chown -R root:root /etc/openvpn/easy-rsa
cd /etc/openvpn/easy-rsa

export EASYRSA_BATCH=1

echo 'set_var EASYRSA_ALGO ec'   | sudo tee -a vars
echo 'set_var EASYRSA_CURVE secp384r1' | sudo tee -a vars

# Initialize
./easyrsa init-pki
```

Crear la CA (Certified Authority)

```bash
# With password
./easyrsa ca-build
# Without password
./easyrsa ca-build nopass
```

- **pki/ca.crt**: Certificado público de la CA (Se comparte).
- **pki/private/ca.key**: Clave privada de la CA (NO se comparte).

Certificado y clave del servidor:

```bash
# Generate CSR & Key
./easyrsa gen-req server nopass
# Sign like a server
./easyrsa sign-req server server
```

- **pki/issued/server.crt**: Certificado del servidor.
- **pki/private/server.key**: Clave privada del servidor.
- **pki/reqs/server.req**: CSR (Ya no se necesita).

Certificados de clientes:

```bash
# Client "laptop1" wihtout pass
./easyrsa gen-req {laptop1} nopass
# Client "laptop1" with pass
./easyrsa gen-req {laptop1}
# Sign client
./easyrsa sign-req client {laptop1}
```

- **pki/issued/laptop1.crt**.
- **pki/private/laptop1.key**.

Clave estática para tls-crypt.

```bash
openvpn --genkey secret ta.key
```

Copiar todo a las rutas de openvpn.

```bash
sudo mkdir -p /etc/openvpn/server
sudo cp pki/ca.crt pki/issued/server.crt pki/private/server.key /etc/openvpn/server/
sudo cp ta.key /etc/openvpn/server/
sudo cp pki/crl.pem /etc/openvpn/server/
```

Plantilla servidor:

```bash
port 1194
proto udp
dev tun

# Certs/keys
ca /etc/openvpn/server/ca.crt
cert /etc/openvpn/server/server.crt
key /etc/openvpn/server/server.key

# Usar ECDHE moderno: (si no usás dh.pem)
# tls-version-min 1.2
# ncp-ciphers TLS-ECDHE-ECDSA-WITH-AES-256-GCM-SHA384:TLS-ECDHE-RSA-WITH-AES-256-GCM-SHA384
# (si usás DHE:)
# dh /etc/openvpn/server/dh.pem

# tls-crypt (una sola key para todos)
tls-crypt /etc/openvpn/server/ta.key

topology subnet
server 10.8.0.0 255.255.255.0

persist-key
persist-tun
user nobody
group nogroup
verb 3

# CRL (si revocás)
# crl-verify /etc/openvpn/server/crl.pem
```

Plantilla cliente

```bash
client
dev tun
proto udp
remote <IP_o_FQDN_del_servidor> 1194
resolv-retry infinite
nobind
persist-key
persist-tun
verb 3

<ca>
# ca.crt content
</ca>
<cert>
# laptop1.crt content
</cert>
<key>
# laptop1.key content
</key>
<tls-crypt>
# ta.key content
</tls-crypt>

```