# Creación de VPC con CLI

## Objetivo de la práctica

En esta práctica vamos a crear la misma VPC que en ejercicios anteriores pero utilizando CLI. Se adjunta un script de ejemplo en el cual se realizan las acciones:

* Creación de una VPC
* Creación de una subred
* Creación de un grupo de seguridad
* Creación de una instancia EC2
* Creación Internet Gateway y guardado de ID
* Se adjunta el IGW a la VPC
* Se crear tablas de rutas y se guardan sus ID
* Se agregan una ruta para salida a internet
* Se asocia la tabla de rutas a la subred


## Práctica a Realizar

Tienes que descargar y modificar el script

[script_UD03](::/script_UD03)

para que cree una VPC con la dirección 192.168.0.0/16 y una subred dentro de esta con la dirección 192.168.0.0/24, luego ejecutas el script. Para poder ejecutarlo tendrás que autenticarte primero con la información
de la sesión actual de tu laboratorio. Comprueba que se crean los elementos indicados anteriormente.

Ahora crea una instancia en otra subred de nombre “subred-tunombre” y haz un ping de una máquina a otra.
Primero deberás conectarte por ssh y hacer un ping de manera local (el ping funciona).
Deberás modificar el grupo de seguridad creado y permitir el protocolo ICMP. Normalmente las instancias tienen grupos de seguridad diferentes, pero en este caso como la configuración es muy sencilla en el nuevo ec2 puedes reutilizar el grupo de seguridad y permitir el ping.
Esta parte se hace desde la consola gráfica de AWS

!!! success "Captura las pantallas"
    Resultado de la ejcución del script

    Mapa de recursos de la vpc creada

    Direcciones ip privadas de las instancias

    Ping de una instancia a la otra
