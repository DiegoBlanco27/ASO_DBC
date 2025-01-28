# Guía Practica 2
- Para mostrar las 5 últimas entradas del historial junto con la hora y estado de ejecución usaremos el comando 
- Con `Get-Command` se muestran todos los comandos disponibles en PowerShell, se puede interrumpirlo pulsando las teclas CTRL-C
- s
- Para mostrar todos los procesos de `msedge` con su identificador, consumo de CPU y sus hilos usaremos el comando 
- El parametro `-Delimiter` de `Export-CSV` sirve para
- Para mostrar todos los comandos que contengan el verbo `Update` 
- Para localizar facilmente la herramienta Recortes en el comando `Get-Process` 
- s
- El parametro `-MemeberType` de `Get-Member` sirve para 
- Para finalizar la ejecucion de un programa desde la línea de comandos en este caso la herramienta Recortes usaremos
- Para mostrar todos los procesos con el nombre `svchost` usaremos
- Para mostrar el número de estancias de `svchost` usaremos
- s
- s
- Para mostrar los usuarios agrupados por `Enabled` usaremos 
- Para mostrar los usuarios con la cuenta habilitada usaremos `Where-Object` y seleccionaremos los que tiene `Enabled` puesta en `True`
- Para mostrar los usuarios que iniciaron sesión usaremos la propiedad

Queremos programar una tarea que se ejecutara una vez a la semana durante las vacaciones de Navidad (del 16 de diciembre al 12 de enero)
El script de la tarea debera comprobar el espacio libre en el directorio raiz del disco y almacenar los datos leídos en un fichero log. Tiene que hacer lo siguiente:
- Obtener el espacio en uso en el directorio raiz. Esto lo puedes hacer mediante el comando "df -h --output==pcent,target". Ten en cuenta que tendras que manipular la salida para quedarte con la parte que te interesa (el porcentaje ocupado en la particion raiz).
- Añadir el fichero "/var/log/disk space_alert.log" un mensaje que puede ser:
  * "YYYY MM-DD HH-MM-SS - ALERTA. Espacio ocupado XX%" si esta ocupado más del 80% del espacio del disco.
  * "YYYY-MM-DD HH-MM-SS - Espacio ocupado XX%" si el espacio es inferior al 80%