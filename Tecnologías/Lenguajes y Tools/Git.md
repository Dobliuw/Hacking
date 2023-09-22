----

# Clonar sub carpetas de un repo 

Ejemplo, tenemos un proyecto que es el de vulhub, si quisieramos clonarnos alguna carpeta del mismo https://github.com/vulhub/vulhub/tree/master/kibana/CVE-2018-17246, podriamos hacer lo sig: 

```shell
# Remplazar donde dice tree/master por /trunk
svn checkout https://github.com/vulhub/vulhub/trunk/master/kibana/CVE-2018-17246
```