# Guía Practica 3
1. Para esta Practica vamos a usar una maquina virtual con Ubuntu Server 22.04, usaremos el box "generic/ubuntu64", y añadiremos desde VirtualBox un adaptador puente.
2. Usaremos una red privada de clase A, por ejemplo la 10.0.0.0/8 con una mascara de subred 255.0.0.0, yo usare la IP; 10.10.0.1, y mis compañeros usaran las siguientes IP: 10.10.0.2; 10.10.0.3; 10.10.0.4.
3. Crearemos en el servidor una cuenta para mi y otra para cada compañero usando el comando adduser.
4. Usaremos el comando ssh -keygen -b para crear claves para los usuarios y pondremos más de 1024 bits para que la clave sea un poco segura y que no sea facil de descifrar.
5. Ahora, intentaremos acceder a nuestro directorio dentro del ordenador de nuestros compañeros, primero haremos ping para comprobar que hay conexion entre los equipos y despues usaremos el comando "scp .ssh/id_rsa.pub diego@10.10.0.4:/home/diego" donde "diego" es nuestro nombre de usuario.
