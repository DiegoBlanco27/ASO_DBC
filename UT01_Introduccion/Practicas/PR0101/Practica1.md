# Guía Practica 1

1. Buscaremos una imagen de Ubuntu Server 20.04 y la cogeremos, en mi caso he escogido la siguiente: "gusztavvargadr/ubuntu-server-2004-lts"
2. Ejecutaremos el comando `vagrant init gusztavvargadr/ubuntu-server-2004-lts` y se nos añadira un Vagrantfile al directorio, que contiene la configuración de la maquina virtual
3. Usaremos el comando `vagrant up` para iniciar la maquina
4. Ahora, iremos al Vagrantfile y escribiremos lo siguiente:
    - Para cambiar el nombre de la maquina virtual a Ubuntu Server pondremos el comando `vb.name = "ubuntu server"` dentro del comando `config.vm.provider "VirtualBox" do |vb|`
    - Para asignarle memoria RAM tendremos que poner dentro del comando `config.vm.provider "VirtualBox" do |vb|` lo siguiente: `vb.memory = 2048` donde el número es los MB que queremos asignarle
    - Para cambiar el número de CPU pondremos dentro de `config.vm.provider "VirtualBox" do |vb|` el comando `vb.cpus = 2` donde el numero es el número de CPUs
    - Para cambiar el nombre del equipo (hostname) pondremos lo siguiente: `config.vm.hostname = "server-dbc"`
    - Para sincronizar una carpeta de la maquina con un directorio usaremos este comando: `config.vm.synced_folder "/data", "PR0101"` Primero pondremos la carpeta de la maquina y luego la del equipo
   
