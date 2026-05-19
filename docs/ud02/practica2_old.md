# Prácticas entregables

## Práctica 1

### Creación de una Máquina Virtual (práctica guiada)

Reproduce la práctica guiada y haz una captura de pantalla en la que se vea la conexión por RDP a la máquina Windows Server 2025 creada.

## Práctica 2

### Creación de una Máquina Linux

Necesitamos una máquina que actúe como **servidor de Bases de Datos** y para ello vamos a crear una instancia EC2.

Queremos que el tamaño de la máquina se adapte a esa función de servidor de Base de Datos. Decide tú qué **familia** de instancias utilizar.

Como sistema operativo utilizaremos **Ubuntu**, y deseamos que al crearse la máquina se **instale automáticamente** el paquete del gestor de base de datos **mysql**.

No vamos a utilizar el par de claves del laboratorio, sino **crear un par de claves nuevo** para conectarnos por ssh. El usuario de conexión será el que nos cree [por defecto](https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/managing-users.html#ami-default-user-names).

!!! tip
    Para instalar mysql hay que actualizar los repositios de Linux y a continuación instalar el paquete con el comando `apt install mysql-server -y`

!!! tip
    Recuerda cambiar los [permisos del fichero de la clave privada](https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/connection-prereqs-general.html#connection-prereqs-private-key) y añadirlo con el parámetro `-i` dentro del comando `ssh`

!!! success "Captura las pantallas"
    Captura las pantallas necesarias en la que se vea el tamaño de la instancia, los datos de usuario y el par de claves utilizado y la conexión por ssh a la máquina Linux.

## Práctica 3

### Creación de una Máquina Linux desde la CLI

Ahora que ya hemos practicado con el entorno gráfico, vamos a comenzar a utilizar la terminal. Para ello, tal y como se explicó en el Tema 1, debemos configurar las credenciales en el archivo `credentials` para poder estar conectados con el lab.

En esta práctica vamos a hacer un script (en Windows o Linux) para crear una máquina virtual con los valores por defecto mediante el [comando `aws ec2 run-instances`](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-ec2-instances.html) .

!!! note "Nota"
    Necesitamos especificar algunos parámetros mínimos, entre ellos el **identificador de la AMI** a utilizar. Existen herramientas y comandos para conocer las IDs de las AMIs, pero nosoros accederemos a la consola gráfica y, al intentar crear una instancia, veremos la ID de la AMI que nos interesa para poder introducirla en el comando.

    Recuerda que como usuario de aws academy debes utilizar la región **us-east-1** que te permite crear los recursos que se piden en este curso.

Crearemos un fichero de script con el siguiente comando:

=== "Windows"
    ```    
    aws ec2 run-instances `
    --image-id ami-0b09ffb6d8b58ca91 `
    --count 1 `     
    --instance-type m1.small `     
    --key-name vockey `     
    --region us-east-1
    ```

=== "Linux"
    ```
    aws ec2 run-instances \
    --image-id ami-0b09ffb6d8b58ca91 \
    --count 1 \
    --instance-type m1.small \
    --key-name vockey \
    --region us-east-1    
    ```

Una vez guardado, damos permiso de ejecución (en Linux) y lo ejecutamos anteponiendo `./` al nombre del script (en Windows y Linux).

Al ejecutarlo, el comando nos devuelve una cadena *json* con información relativa a la instancia creada, pero no nos aparece ni la IP Pública ni el nombre DNS Público asignados.

Para poder ver dicha información y así poder conectarnos mediante ssh, ejecutamos el comando `aws ec2 describe-instances` y filtramos la información de salida para que nos aparezca la palabra `PublicIpAddress`. En este caso **no vamos a conectarnos por SSH** pues en el script sería necesario abrir el puerto 22 en el grupo de seguridad. Lo veremos en el siguiente tema.

!!! success "Captura las pantallas"
    Captura las pantallas necesarias en la que se vea el comando de creación de la instancia.

## Práctica 4

### Creación de una Máquina Linux desde la CLI

Modifica el script de la práctica anterior para lanzar una nueva instancia cuyo tamño sea `t2.micro`, la AMI sea una basada en Debian y el par de claves sea el creado en la práctica 2.

!!! success "Captura las pantallas"
    Captura las pantallas necesarias en la que se vea el script y la ejecución del mismo.

---

## Liberación de recursos

Una vez finalizada la práctica hay que eliminar los recursos creados para que no nos consuman crédito:

- Termina todas la instancias. En el panel de EC2, con las instancias seleccionadas, pulsamos sobre la Acción **Terminar (eliminar) instancia**. Nos informa que el volumen EBS asociado también se eliminará.

Recuerda finalizar el laboratorio cuando acabes con las prácticas.
