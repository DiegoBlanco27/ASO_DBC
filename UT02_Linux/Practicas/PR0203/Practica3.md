# Guía Practica 3
1. Para esta Practica vamos a usar una maquina virtual con Ubuntu Server 22.04, usaremos el box "generic/ubuntu64", y añadiremos desde VirtualBox un adaptador puente.
2. Usaremos una red privada de clase B, como por ejemplo 10.10.0.1, y los compañeros usaran las siguientes IP: 10.10.0.2; 10.10.0.3; 10.10.0.4.
3. Crearemos en el servidor una cuenta para mi y otra para cada compañero usando el comando adduser.
4. Usaremos el comando ssh -keygen -b para crear claves para los usuarios y pondremos por ejemplo, 1024 para que no sea una clave ni muy facil ni muy compleja.
5. Ahora, intentaremos acceder a nuestro directorio dentro del ordenador de nuestros compañeros, primero haremos ping para comprobar que hay conexion entre los equipos y despues usaremos el comando "scp .ssh/id_rsa.pub diego@10.10.0.4:/home/diego" donde "diego" es nuestro nombre de usuario.
