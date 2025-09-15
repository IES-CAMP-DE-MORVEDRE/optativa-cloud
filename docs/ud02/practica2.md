# Prácticas entregables

## Práctica 1
### Creación de una Máquina Virtual (práctica guiada)

Reproduce la práctica guiada y haz una captura de pantalla en la que se vea la conexión por RDP a la máquina Windows Server 2025 creada.

## Práctica 2
### Creación de una Máquina Linux

Necesitamos una máquina que actúe como servidor de Bases de Datos y para ello vamos a crear una instancia EC2.

Queremos que el tamaño de la máquina se adapte a esa función de servidor de Base de Datos. Decide tú qué familia de instancias utilizar. 

Como sistema operativo utilizaremos Ubuntu, y deseamos que al crearse la máquina se instale automáticamente el paquete del gestor de base de datos **mysql**.

No vamos a utilizar el par de claves del laboratorio, sino crear un par de claves nuevo para conectarnos por ssh. El usuario de conexión será el que nos cree [por defecto](https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/managing-users.html#ami-default-user-names).

!!! tip
    Para instalar mysql hay que actualizar los repositios de Linux y a continuación instalar el paquete con el comando `apt install mysql -y`


!!! tip
    Recuerda cambiar los [permisos del fichero de la clave privada](https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/connection-prereqs-general.html#connection-prereqs-private-key) y añadirlo con el parámetro `-i` dentro del comando `ssh`

!!! success "Captura las pantallas"
    Captura las pantallas necesarias en la que se vea el tamaño de la instancia, los datos de usuario, el par de claves utilizado y la conexión por ssh a la máquina Linux.

## Práctica 3
### Creación de una Máquina Linux desde la CLI
