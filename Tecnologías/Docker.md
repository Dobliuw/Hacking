![[Pasted image 20230215163522.png]]

----

# Docker Cheat Sheet

```shell
docker --version
# Para ver la información de la instalación de docker.
docker info
# Información de la instalación de docker.
docker run {image_name}
# Crea y ejecuta un contenedor.
docker ps 
# Listar los contenedores desplegados corriendo en el sistema.
docker ps -a 
# Listar TODOS los contenedores, corriento, parados, matados, etc.
docker inspect {container_ID}
# Esto es para ver la configuración de el contenedor.
docker run --name {whatever} {image_name}
# Crar, ejecutar un contenedor a raiz de una imagen asignandole al contenedor un nombre 
docker rename {prev_name} {new_name}
# Renombrar un contenedor.
docker rm {container_ID/container_name}
# Eliminar un contenedor
docker rm -f $(docker ps -a)
# Eliminar de manera forzadas todos los contenedores corriendo o no del sistema.
docker exec 
# Ejecutar comando o proceso en un container.
docker run -p {us_port}:{docker_port} -d {image_name}
# Crear y ejecutar un contenedor enlazando un puerto de nuestra maquina con un puerto del contenedor (-p 80:80) a la vez que corriendolo en segundo plano (-d = detach)
docker logs {container_name/container_id}
# Ver logs de un container
docker logs --tail 10 -f {container_name/container_id}
# Ver en tiempo real (-f = follow) las ultimas 10 lineas de los logs (--tail 10)
docker run -it -v /{os_path}:/{docker_path} {image_name}
# Crear y ejecutar un contenedor de manera interactiva con una terminal (-it) montando la ruta "os_path" en la ruta "docker_path" (-v /example.txt:/exampleDir)
docker volume ls 
# Listar volumenes
docker volume create {volume_name}
# Crear volumen
docker network ls
# Crear una imagen a partir de un dockerfile
docker build -t {image_name} {path_dockerfile}
# Listar conexiones de las redes
docker network create {name}
# Crear una red
docker network create --atachable {name}
# Crear una red a la que otros contenedores se puedan conectar.
docker network inspect {name}
# Inspeccionar una red.
docker network connect {network} {container}
# Conectar un container a una red
docker image ls 
# Listar iamgenes
docker pull {image_name}
# Traer una imagen del repo de docker hub.
docker images --fillter "dangling=true" -q
# Sacar los id's de las imagenes <none> 
```


## Dockerfile 

```Dockerfile 
 FROM ubuntu:latest 
 # Version de la imagen
 MAINTAINER Owen Bonoris aka Dobliuw "dobliuw@dobliuw.com"
 
 ENV DEBIAN_FRONTEND noninteractive
 # Para que no entre en modo interactivo
 RUN apt update && apt install -y net-tools \ 
   iputils-ping \ 
   curl \ 
   git \ 
   nano \ 
   apache2 \ 
   php
 # Comandos que quiero ejecutar a la hora de crear la imagen 
 EXPOSE 80 
 # Exponer el puerto 80 del contenedor
 ENTRYPOINT service apache2 start && /bin/bash 
 # Cuando se inicie que levante el demon de apache2 y el /bin/bash para evitar errores
```