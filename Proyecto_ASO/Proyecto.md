# Proyecto de la 1º Evaluación 
## Análisis de redes 
### Indice
   - Creación de la VM y del script
   - Solicitud de dirección IP
   - Comando ping
   - Escaneo de puertos
   - Identificación del SO
   - Recopilación de la información
   - Opciones Adicionales (MAC y marca de tiempo)
   - Script
   - Pruebas de funcionamiento

### Procedimiento
- Crearemos una maquina virtual con un ubuntu por ejemplo `generic/ubuntu2204`
- Crearemos el script y le pondremos de nombre por ejemplo `analisis_red.sh`
- Lo primero que hay que poner en el script es `#!/bin/bash` y a continuación empezaremos con los parametros necesarios:
  1. Solicitaremos una dirección IP al usuario: `read -p "Introduce tu dirección IP:" IP`
  2. A continuación, haremos `ping` a todas las direcciones red para saber si esta IP pertenece a un equipo: `echo "Realizando ping a $IP ..."` `if ping -c 1 $IP &> /dev/null; then` `echo "El equipo con IP $IP está activo."` `else` `echo "No se recibió respuesta del equipo con IP $IP."` `exit 1` `fi`
  3. Ahora, realizaremos un escaneo de puertos para ver cuales estan abiertos, usando el comando `nc` y guardaremos el número de puerto y su servicio: `echo "Escaneando puertos abiertos en la dirección $IP..."` `puertos_abiertos=""` `for puerto in {1..1024}; do` `nc -z -v 1 $IP $puerto &> /dev/null` `if [ $? -eq 0 ]; then` `servicio=$(grep -w $puerto /etc/services | awk '{print $1}' | head -n 1)` `puertos_abiertos+="$puerto ($servicio)\n"` `fi` `done` `if [ -z "$puertos_abiertos" ]; then` `echo "No se encontraron puertos abiertos en el rango 1-1024."` `else` `echo -e "Puertos abiertos encontrados:\n$puertos_abiertos"` `fi`
  4. Identificaremos el sistema operativo del equipo usando el valor TTL de los mensajes ping ya que los sistemas Windows tienen un TTL de 128 (o menos) y los de Linux de 64 (o menos): `echo "Identificando el sistema operativo..."` `TTL=$(ping -c 1 $IP | grep -oP "ttl=\K[0-9]+")` `if (( TTL >= 100 && TTL <= 128 )); then``so="Windows"` `elif (( TTL >= 30 && TTL <= 64 )); then` `so="Linux"` `else` `so="Desconocido"` `fi` `echo "Sistema operativo: $so"`
  5. Toda la información que hemos recopilado se mostrara en pantalla y se guardara en un archivo cuyo nombre indicara el usuario: `read -p "Introduce el nombre del archivo para guardar la información: " archivo_salida` `echo "Guardando resultados en $archivo_salida..."` `echo -e "Análisis de red para la IP $IP:\n" > $archivo_salida` `echo "Dirección MAC: $mac_address" >> $archivo_salida` `echo "Sistema operativo: $so" >> $archivo_salida` `echo -e "Puertos abiertos:\n$puertos_abiertos" >> $archivo_salida` `echo "Análisis completado. Resultados guardados en $archivo_salida."`
  6. A mayores, mostraremos la MAC del equipo escaneado usando el comando `arp`: `echo "Obteniendo la dirección MAC de $IP ..."` `mac_address=$(arp -n $IP | grep "$IP" | awk '{print $3}')` `if [ -z "$mac_address" ]; then` `mac_address="MAC no disponible"` `fi` `echo "Dirección MAC: $mac_address"` 
  7. También mostraremos el tiempo que se ha tardado en realizar el escaneo usando `$SECONDS` que mostrara el tiempo transcurrido en segundos: `duracion=$SECONDS` `echo "Escaneo realizado en $duracion segundos."`

### Script
#!/bin/bash

read -p "Introduce tu dirección IP:" IP

echo "Realizando ping a $IP ..."
if ping -c 1 $IP &> /dev/null; then
    echo "El equipo con IP $IP está activo."
else
    echo "No se recibió respuesta del equipo con IP $IP."
    exit 1
fi

echo "Obteniendo la dirección MAC de $IP ..."
mac_address=$(arp -n $IP | grep "$IP" | awk '{print $3}')

if [ -z "$mac_address" ]; then
    mac_address="MAC no disponible"
fi

echo "Dirección MAC: $mac_address"

echo "Escaneando puertos abiertos en la dirección $IP..."
puertos_abiertos=""
for puerto in {1..1024}; do
    nc -z -v 1 $IP $puerto &> /dev/null
    if [ $? -eq 0 ]; then
        servicio=$(grep -w $puerto /etc/services | awk '{print $1}' | head -n 1) 
        puertos_abiertos+="$puerto ($servicio)\n"
    fi
done

if [ -z "$puertos_abiertos" ]; then
    echo "No se encontraron puertos abiertos en el rango 1-1024."
else
    echo -e "Puertos abiertos encontrados:\n$puertos_abiertos"
fi

echo "Identificando el sistema operativo..."
TTL=$(ping -c 1 $IP | grep -oP "ttl=\K[0-9]+")
if (( TTL >= 100 && TTL <= 128 )); then
    so="Windows"
elif (( TTL >= 30 && TTL <= 64 )); then
    so="Linux"
else
    so="Desconocido"
fi
echo "Sistema operativo: $so"

read -p "Introduce el nombre del archivo para guardar la información: " archivo_sa>echo "Guardando resultados en $archivo_salida..."

echo -e "Análisis de red para la IP $IP:\n" > $archivo_salida
echo "Dirección MAC: $mac_address" >> $archivo_salida
echo "Sistema operativo: $so" >> $archivo_salida

duracion=$SECONDS

echo "Análisis completado. Resultados guardados en $archivo_salida."
echo "Escaneo completado en $duracion segundos."
echo "Resultados guardados en $archivo_salida."

### Pruebas
  - Los caracteres mostrados `de esta forma` son los introducidos por el usuario el resto los ha generado el script
  * Equipo Linux
    - vagrant@ubuntu2204:~$ `./analisis_red.sh`
    - Introduce tu dirección IP:`10.0.2.2`
    - Realizando ping a 10.0.2.2 ...
    - El equipo con IP 10.0.2.2 está activo.
    - Obteniendo la dirección MAC de 10.0.2.2 ...
    - Dirección MAC: 52:54:00:12:35:02
    - Escaneando puertos abiertos en la dirección 10.0.2.2...
    - No se encontraron puertos abiertos en el rango 1-1024.
    - Identificando el sistema operativo...
    - Sistema operativo: Linux
    - Introduce el nombre del archivo para guardar la información: `prueba1`
    - Guardando resultados en prueba1...
    - Análisis completado. Resultados guardados en prueba1.
    - Escaneo completado en 18 segundos.

  * Equipo Windows 
    - vagrant@ubuntu2204:~$ `./analisis_red.sh`
    - Introduce tu dirección IP:`192.168.110.11`
    - Realizando ping a 192.168.110.11 ...
    - El equipo con IP 192.168.110.11 está activo.
    - Obteniendo la dirección MAC de 192.168.110.11 ...
    - Dirección MAC: 64:4E:D7:68:6F:0D
    - Escaneando puertos abiertos en la dirección 192.168.110.11...
    - No se encontraron puertos abiertos en el rango 1-1024.
    - Identificando el sistema operativo...
    - Sistema operativo: Windows
    - Introduce el nombre del archivo para guardar la información: `prueba2`
    - Guardando resultados en prueba2...
    - Análisis completado. Resultados guardados en prueba2.
    - Escaneo completado en 17 segundos.
  
  * Resultados
    - Prueba 1
      
      vagrant@ubuntu2204:~$ `cat ./prueba1`
      
      Análisis de red para la IP 10.0.2.2:

      Dirección MAC: 52:54:00:12:35:02

      Sistema operativo: Linux

      Puertos abiertos:
    
    - Prueba 2

      vagrant@ubuntu2204:~$ `cat ./prueba2`
      
      Análisis de red para la IP 192.168.110.11:

      Dirección MAC: 64:4E:D7:68:6F:0D

      Sistema operativo: Windows

      Puertos abiertos: