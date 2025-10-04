# Práctica 3. Creación de VPC con CLI 

## Objetivo de la práctica

En esta práctica vamos a crear la misma VPC que en ejercicios anteriores pero utilizando CLI. Se adjunta un script de ejemplo en el cual se realizan las acciones:

* Creación de una VPC.
* Habilitar DNS en la VPC.
* Creación de una subred.
* Creación de un grupo de seguridad y apertura de un puerto.
* Creación de una instancia EC2.
* Creación Internet Gateway y guardado de ID.
* Se adjunta el IGW a la VPC.
* Se crear tablas de rutas y se guardan sus ID.
* Se agregan una ruta para salida a internet.
* Se asocia la tabla de rutas a la subred.


## Práctica a Realizar

Tienes que descargar el siguiente script:

=== "Linux"
    [script Creación VPC para Linux](script_UD03.sh)

=== "Windows"
    [script Creación VPC para Windows](script_UD03.ps1)

### Parte 1. Modificación del script de creación de la VPC y la EC2

La práctica consiste en modificar el script para que la VPC la cree con la dirección `192.168.0.0/16` y la subred que hay dentro de ella la cree con la dirección `192.168.3.0/24`. 

!!! warning "Atención"
    Fíjate que la instancia EC2 del script de ejemplo se crea con una IP fija dentro de la subred.

Ejecuta el script. Para poder ejecutarlo tendrás que autenticarte primero con la información de la sesión actual de tu laboratorio. Comprueba que se crean los elementos indicados anteriormente.

### Parte 2. Creación de una subred y otra máquina EC2
**Esta parte se hace desde la consola gráfica de AWS**

Debes crear una instancia EC2 en otra subred de nombre “*subred-tunombre*” y hacer un ping de una máquina a otra.

Para comrpbar el ping, rimero deberás conectarte por ssh a la primera máquina y hacer un ping a la segunda máquina de manera local (el ping funciona).

Deberás modificar el grupo de seguridad creado y permitir el protocolo ICMP. Normalmente las instancias tienen grupos de seguridad diferentes, pero en este caso como la configuración es muy sencilla, en la nueva máquina EC2 puedes reutilizar el grupo de seguridad y permitir el ping.


!!! success "Captura las pantallas"
    Resultado de la ejcución del script

    Mapa de recursos de la vpc creada

    Direcciones ip privadas de las instancias

    Ping de una instancia a la otra
