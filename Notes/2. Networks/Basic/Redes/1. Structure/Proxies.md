----
- Tags: #redes #basico #teoria 
----
# Proxies 

Un proxy es cuando un dispositivo o servicio se ubica en medio de una conexión y actúa como mediador. el mediador es la pieza de información crítica porque significa que el dispositivo en el medio debe poder inspeccionar el contenido del tráfico. Sin la capacidad de ser mediador, el dispositivo estécnicamente una puerta de enlace, no un proxy.

Existen muchos tipos de servicios proxy, pero los principales son:

- Dedicated Proxy / Forward Proxy
- Reverse Proxy
- Transparent Proxy 
#### Dedicated Proxy / Forward Proxy 

El *Forward Proxy* es lo que la mayoría de gente imagina cuando se habla de proxy. Un Fordward Proxy es cuando un cliente realiza una solicitud a una computadora y esa computadora lleva a cabo la solicitud.

Por ejemplo, en una red corporativa, es posible que las computadores sensibles no tengan acceso directo a internet. Para acceder a un sitio web, deben pasar por un proxy (O filtro web). Esta puede ser una línea de defensa contral el malware increiblemente poderosa, ya que no solo se necesitaría eludir el filtro web, si no que también se necesitaría tener en cuenta el proxy. 

Los navegadores como Internet explorer (ahora Edge) o Chrome obedecen a la configuración de *Sysmte Proxy* por defecto. Si el malware utiliza WinSock (API nativa de Windows), probablemente será compatible con el proxy si ningún código adicional. Firefox por ejemplo, no usa WinSock y en su lugar usa libcurl, lo que le permite usar el mismo código en cualquier sistema operativo. Esto significa que el malware necesitaría buscar Firefox y extraer las configuraciones del proxy, lo cual es muy poco probable que realize.

Alternativamente, el malware podría utilizar DNS como mecanismo de C2, pero si una organización está monitoreando DNS (Lo cual se hace fácilmente usand Sysmon), este tipo de tráfico debería quedar detectado rápidamente.

Otro ejemplo de Forward Proxy es [[Burpsuite]], ya que la mayoría de la gente lo utiliza para reeenviar solicitudes HTTP. Sin embargo, esta aplicación es la navaja suiza de los servidores proxy HTTP y puede configurarse para que sea un *reverse proxy* o *transparent*. 

![[Foward_proxy.png]]

#### Reverse Proxy 

Un *reverse proxy* (Proxy inverso) es lo opuesto a un forward proxy. En lugar de etar diseñado para filtrar las solicitudes salientes, filtra las entrantes. El objetivo más común de un proxy inverso es escuchar una dirección y reenviarla a una red cerrada.

Muchas organizaciones utilizan CloudFlare porque tiene una red sólida que puede resistir la mayoría de los ataques DDoS. Al utilizar CloudFlare, las organizaciones tiene una forma de filtrar la cantidad (Y el tipo) de tráfico que se envía a sus servidores.

Los pentesters configurarán servidores proxy inversos en los endpoints infectados. El endpoint infectado escuchará en un puerto y enviará cualquier cliente que se conecte al puerto al atacante a través del endpoint infectado. Esto es útil para eludir firewalls o evadir el registro. Las organizaciones pueden terner DIS (Instrusion Detection Systems), que vigilan las solicitudes web externas. Si el atacante obtiene acceso a la organización a través de SSH, un proxy inverso puede enviar soliciutdes web a través del túnel SSH y evadir el IDS.

Otro proxy inverso común es ModSecurity, un firewall de aplicaciones web (WAF). Los firewallss de aplicaciones web inspeccionan las solicitudes web en busca de contenido malicioso y bloquean la solicitud si es malicioso. 

![[reverse_proxy.png]]

#### (Non-) Transparent Proxy

Todos estos servicios de proxy actúan de forma transparente (Transparent) o no transparente (Non-transparent).

Con un *transparent proxy*, el cliente no sabe de su existencia. El proxy transparente intercepta las solicitudes de comunicación del cleinte a Internet y actúa como una instancia sustituta. Haci el exterior, ell proxy transparente, al igua lque el proxy no transparente, actúa como interlocutor de comunicación.

Con un *non-transparent proxy*, debemos ser informados sobre su existencia. Para ello, tanto nosotros como al software que queremos utilizar se le hes dado una configuración especial del proxy para asegurarnos de que el trafico a internet se dirja primero al proxy. Si esta configuración no existe, no podremos comunicarnos mediante el proxy. Sin embargo, dado que el proxy suele proporcionar la única ruta de comunicación con otras redes, la comunicación a Internet generalmente se corta sin una configuración de proxy correspondiente. 