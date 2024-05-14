# DSQUERY

El comando `dsquery` será utilizado para realizar consultas en un servicio de Active Directory, está permite a los administradores buscar por objetos dentro del AD y obtener información especifica sobre estos objetos.
###### Objetct Types

Los tipos de objetos que nos podemos encontrar en un entorno de Active Directory son:

- **User**: Representa cuentas de usuarios dentro del Active Directory.
- **Computer**: Representa objetos de computadora, lo que incluye workstations, servers y otros dispositivos ingresados en el dominio.
- **Group**: Representa grupos de seguridad o listas de distribuciones usadas para la gestión de permisos y control de accesos.
- **OU** (**Organizational Unit**): Representa unidades organizativas, las cuales son contenedores usados para la organización y administración de objetos dentro de la jerarquía de Active Directory.
- **Contact**: Representa objetos de contacto, usalmente usados para almacenar información sobre contactos o recursos externos .
- **Server**: Representa objetos de servidor dentro del dominio.
- **Site**: Representa sitios del Active Directory, que son agrupaciones lógicas de recursos de red basados topologias físicas o de redes.
- **Subnet**: Representa las IPs de subredes utilizadas por el direccionamiento y enrutamiento de la red.
- **Printer**: Representa objetos de impresoras dentro del dominio.
- **Quota**: Representa objetos de cuota utilizados para administrar el uso y la signación del espacio en disco.
- **Trust**: Representa relaciones de confianza entre dominios o bosques.
- **Partition**: Representa objetos de particiones, las cuales son divisiones logicas de la base de datos de Active Directory.

```powershell
# Search all users and limit the result in just 10 (0 for no limits)
> dsquery user "DC=dobliuw,DC=com" -limit 10
# Search for a user
> dsquery user -name Owen
# Find all users in a organizational unit (ou)
> dsquery user "ou=Cibersecurity,dc=dobliuw,dc=com"
# Search for computers with specific atributes
> dsquery computer -name "DESKTOP-*" -attr operatingSystem
# Find groups with specific members
> dsquery group -member "CN=Owen Nicolas,CN=Users,DC=dobliuw,DC=com"
# Retrieve specific attributes for user
> dsquery user -name Owen -attr samAccountName giveName sn mail
# Search for all domain controllers
> dsquery server -domain {domain_name} -isgc
# List all OU in the domain
> dsquery ou
# Find subnets associated with a site
> dsquery subnet -site "dobliuwSite"
```