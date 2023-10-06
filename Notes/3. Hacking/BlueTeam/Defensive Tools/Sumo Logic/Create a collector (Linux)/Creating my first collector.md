---------------------
-  Tags: #teoria #practica #blue #basico
---------------------
# Descargar el collector
Como vimos anteriormente en [[2. Collectors, Sources & Metadata]], los collectors son pequeños softwares que permite hacer uso de un **source** para recopilar información almanecada en sistemas, en este caso usaremos **Linux**, por lo que habría que descargar el collector desde la aplicación de **Sumo Logic**, el cual es un script en bash.

```bash
chmod +x {collector_downloaded}

sudo ./{collector_downloaded} -q -Vsumo.token_and_url={installationToken}
```
Importante tener en cuenta que el **{installationToken}** se crea también desde la aplicación de **Sumo Logic** en el apartado de tokens. 
Este comando para instalar el collector fue sacado de la [documentación de sumo (Install Collector for Linux)](https://help.sumologic.com/docs/send-data/installed-collectors/linux/#install-using-the-command-line-installer) en donde nos brinda una guia de installación mediante línea de comandos, interfaz gráfica, haciendo uso de token, con ID y access key, etc. 
Cabe destacar que el parametro `-Vsources=<absolute_filepath>` que nos indica que podemos agragar es perteneciente al **source** que utilizara el collector, el cual puede ser creado desde la página de Sumo Logic o ser obtenido (Este será un JSON) y agregado haciendo uso de este parametro. En caso de dudas podemos visitar la [documentación de sumo (Building the Source JSON Configuration file)](https://help.sumologic.com/docs/send-data/use-json-configure-sources/building-source-json-configuration-file/) una vez más. 

Una vez ejecutado el comando anterior, en caso de que hayamos agregado la flag `-Vsources={path_to_source_JSON}` lo que estaremos haciendo es adicionalmente iniciar la instalación del **collector** con el **source** ya asignado, en caso de no haberla agregado de igual manera estaremos dand comienzo a la instalación, la cual creara el collector en la ruta **/opt/SumoCollector/collector**, el cual podremos ejecutar el panel de ayuda para validar las opciones que posee. 

```bash
/opt/SumoCollector/collecotr --help 
```
A su vez, una vez instalado el mismo, en nuestro panel de sumo collector podremos ver nuestro collector activo filtrando por **Installed Collectors**, en caso de haber indicado el source en la instalación podremos comenzar a ver logs y registros en caso de que los haya en el path indicado en el source.
En caso de que no hayamos instalado el collecor indicando un source en formato JSON, podremos una vez visualizado el collector en nuestro panel de Sumo Logic, selesccionar la opción **Add Source** en donde podremos indicarle un nombre entre otras configuraciones así como también aclarar el path de nuestro sistema que queremos que monitoree, por ejemplo **/var/log/apache2/\*.log**. En caso de crear un collector con un source con el path mencionado, este vinculara todos los logs de los archivos **access.log** y **error.log** de apache2 permitiendonos filtrar con querys de Sumo Logic en nuestro panel.



