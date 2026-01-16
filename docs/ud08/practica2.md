# Práctica 2. Alarmas en CloudWatch

Creación de alarmas asociadas a EC2

## Objetivo de la práctica

* Crear una alarma básica en CloudWatch.
* Entender los estados de una alarma (OK / ALARM / INSUFFICIENT_DATA).
* Ver cómo una alarma reacciona ante un cambio de carga.

## Práctica a realizar

### Creación de una instancia EC2

1.- Vamos a utilizar la instancia *Servidor-Web* utilizada en la práctica anterior.

---

### Creación de una alarma en CloudWatch

2.- Accede al servicio **CloudWatch**:

- En el panel lateral accede al menú **Alarmas** --> **Todas las Alarmas**
- Pulsa sobre **Crear Alarma**
- Selecciona una métrica.
    - De las métricas disponibles selecciona las de **EC2**.
    - Pulsa sobre **Métricas por instancia**.
    - Selecciona la métrica **CPUUtilization** asociada a la instancia *Servidor-Web* (se puede filtar por *InstanceId*).
- Una vez aparezca el gráfico, vamos a configurar las siguientes condiciones:
    - Estadística: **Media**
    - Periodo: **1 minuto**
    - Tipo de límite: **Estático**
    - Cuando la CPUUtilization sea...: **Mayor que 70**
    - En la **Configuración adicional** selecionamos que la alarma se disparará cuando haya 2 puntos por encima del límite en 2 muestras consecutivas (**2 de 2**).
- La siguiente pantalla nos pide configurar la **acción** a realizar cuando se dispare la alarma:
    - Cofiguramos una notificación por el servicio SNS:
        - El activador: **En modo alarma**
        - Enviar una notificación al tema de SNS: **Crear un tema nuevo**
        - Introducimos un nombre de tema (o dejamos el por defecto)
        - Añadimos nuestra dirección de correo.
        - Agregamos la notificación.
        - Nos debe llegar un correo electrónico a la dirección especificada para confirmar la suscripción al tema.
- Por último damos un nombre a la alarma y opcionalmente un texto en formato Markdown con la descripción.

<br>

---

### Estrés de la máquina

3.- Vamos a estresar la máquina para que si dispare una alarma:

- Accede por SSH a la máquina EC2
- Instala el paquete *stress-ng*: `sudo apt install -y stress-ng`
- Ejecuta el siguiente comando para estresar la CPU durante 3 minutos: `stress-ng --cpu 4 --timeout 3m`
- Accede al panel de la alarma recién creada y comprueba la información que va mostrando la métrica.
- Si todo ha ido bien, pasados unos minutos debes haber recibido un correo electrónico notificando la alarma.


!!! success "Captura la pantalla"
    Captura la pantalla en la que se vea el panel de la alarma, con la zona roja en el momento del estrés, y otra captura con el correo recibido.

!!! note "Interpretación de la gráfica"
    Es posible que veamos en la gráfica que el % de utilización de la CPU no ha alcanzado la línea roja (70%) y en cambio sí que se ha disparado la alarma. Esto es debido a que el gráfico saca medias cada 5 minutos, y en cambio la alarma está muestreando cada minuto, lo que puede dar lugar a situaciones de que durante 2 minutos la máquina está al 100% y por tanto se dispara la alarma, pero en el conjunto de los 5 minutos la utilización no ha llegado al 70% en total.

<img src="../images/ud08/practica2/ud08_p01.png">
