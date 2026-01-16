# Práctica 1. Métricas EC2

Análisis métricas EC2

## Objetivo de la práctica

* Identificar las métricas básicas de una instancia EC2.
* Consultar métricas desde:
    * La pestaña **Monitoreo** de EC2.
    * El servicio Amazon CloudWatch.
* Comprender la relación entre EC2 y CloudWatch.
* Diferenciar entre monitorización básica y monitorización detallada.

## Práctica a realizar

### Creación de una instancia EC2

1.- Inicia sesión en la Consola de AWS y entra en el servicio **EC2**. Lanza una nueva instancia:

- Llámala *Servidor-Web*
- La imagen será la AMI de Ubuntu.
- El tamaño será un tipo de instancia *t3.micro*.
- El par de claves utilizaremos el del laboratorio (*vockey*).
- Nos aseguramos que se asigna una IP Pública para poder conectarnos desde Internet.
- Nos aseguramos que se crea una regla de firewall para permitir las conexiones por el puerto SSH (22) y HTTP(80).
- Para hacer que durante el primer lanzamiento de la instancia se instale el **servidor HTTP** y se copie el repositorio [hello-cloud](https://github.com/IES-CAMP-DE-MORVEDRE/hello-cloud) ponemos las siguientes líneas en el apartado de **Datos de usuario**:

```bash
#!/bin/bash
apt update
apt install -y apache2
git clone https://github.com/jrpellicer/hello-cloud.git
cp hello-cloud/* /var/www/html -R
```

<br>

---

### Monitorización desde EC2 (pestaña Monitoreo)

2.- Selecciona la instancia creada. Accede a la pestaña **Monitoreo** y observa las métricas que vienen por defecto. Nos interesan:

- CPU Utilization
- Network In 
- Network Out

Pulsa sobre **Administrar el monitoreo detallado** para habilitar que los datos se muestreen cada minuto.

!!! warning "Atención"
    Las métricas básicas son gratuitas, pero al habilitar el monitoreo detallado se nos incrementará el costo del servicio CloudWacth.

Podemos personalizar también la unidad de tiempo que deseamos mostrar y el tiempo de refresco del panel (por defecto el refresco debe ser manual).

!!! note "Nota" 
    Observa que los gráficos ya existen sin haber configurado nada.

!!! info "Explicación"
    EC2 envía automáticamente métricas básicas a CloudWatch. Los gráficos que estamos viendo se alimentan de las métricas de Cloudwatch

---

### Monitorización desde Cloudwatch

3.- Accede al servicio **CloudWatch**:

- En el panel lateral accede al menú **Métricas** --> **Todas las Métricas**
- Dentro de la pestaña **Examinar** nos aparecen cajas con acceso a las métricas y a los paneles automáticos por servicio.
- Accede a **Ver el panel automático de EC2**.
- Observa que nos aparecen prácticamente los mismos gráficos que en la pestaña de **Monitoreo** de EC2, pero en este caso para todas las instancias que hay en ejecución. En uno de los paneles selecciona la instancia *Servidor-Web* y comprueba que los datos coinciden con los vistos anteriormente.


<br>

---

4.- Vamos a crear un nuevo panel:

- En el panel lateral de CloudWatch accede a Paneles.
- Pulsa sobre **Crear un panel**
- Dale un nombre: *Servidor-Web*
- Comienza añadiendo un widget de métrica de tipo **Línea**
- De las métricas disponibles selecciona las de **EC2**.
- Pulsa sobre **Métricas por instancia**.
- Selcciona una métrica asociada a la instancia *Servidor-Web* (se puede filtar por *InstanceId*).
- Una vez añadido el widget, pulsa sobre el botón **+** y añade varios más. Puedes probar varios tipos de widget.


!!! success "Captura la pantalla"
    Captura la pantalla en la que se vea el panel creado con varios widgets .

!!! warning "No borres ningún recurso"
    Puesto que vamos a utilizar la instancia EC2 en la siguiente práctica, no borres ningún recurso creado en esta práctica.
