# Guía Practica 2 (No acabada)
- Preparación de la maquina y configuración de la red.
1. Para esta Practica usaremos un box de ubuntu llamado `generic/ubuntu2204`, tras instalarlo, en la interfaz de VirtualBox añadiremos otro adaptador de red, un adaptador solo anfitrión, que nos servira para interconectar el equipo con la maquina.
2. En el Panel de Control > Centro de redes y recursos compartidos, seleccionaremos "Cambiar configuración del adaptador, seleccionamos el de VirtualBox y le daremos a "Detalles" para ver la dirección IP en mi caso; 192.168.56.1. En la maquina para ver la IP asignada tendremos que usar el comando `ip a`, y buscaremos el adaptador Solo anfitrión, mi dirección IP es; 127.0.0.1 .
3. Para comprobar la conectividad entre el anfitrión y la maquina haremos ping desde nuestro equipo a la maquina usando el comando `ping ` y luego haremos lo mismo desde la maquina al equipo con el comando `ping 192.168.56.1`.
4. Para cambiar el hostname de la maquina a "server-dbc" usaremos el comando `sudo hostnamectl set-hostname 'server-dbc'`.
- Creación del usuario y conexión SSH.
1. Para crear un usuario usamos el comando `sudo adduser "nombre"` en este caso `sudo adduser dbc_server`. 
2. "Pendiente"
3. "Pendiente"
- Conexion transparente a Github.
"Pendiente"