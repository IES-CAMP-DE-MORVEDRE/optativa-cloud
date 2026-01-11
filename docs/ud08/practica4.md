# Práctica 4. Métricas RDS en CloudWatch

Análisis métricas RDS

## Objetivo de la práctica

* Identificar las métricas básicas de una instancia RDS.
* Crear un panel.
* Estresar una base de datos y analizar sus métricas.

## Práctica a realizar

### Creación de una Base Datos RDS

1.- Inicia sesión en la Consola de AWS y entra en el servicio **RDS**. Crea una nueva base de datos pública:

- Seleccionamos el método de *creación estándar*.
- Como motor de base de datos elegimos **MySQL**.
- La plantilla sobre la que se va a basar será **Entorno de pruebas** (las demás no son aptas para el laboratorio).
- Disponibilidad Implementación de una instanciade base de datos de zona de disponibilidad única (1 instancia)
- Ponemos un nombre de servidor que debe ser único en nuestra cuenta de AWS. Introduce uno que lleve tu nombre o iniciales.
- Asignamos nombre de usuario administrador y su contraseña.
- Dejamos las opciones por defecto del tamaño de la instancia y el almacenamiento.
- No vamos a conectar nuestra BBDD a ninguna instancia EC2, y dejamos la BBDD en la VPC por defecto (*Default VPC*).
- **Importante**: Permitimos el *Acceso Público* a nuestra BBDD. Esto generará una IP Pública para poder conectarnos desde Internet.
- Creamos un nuevo *grupo de seguridad*, por ejemplo *bbdd-sg*
- Los demás campos los dejamos por defecto.
<br>

---

### Conexión a la BBDD

2.-	En nuestra máquina local establacemos una conexión mediante un cliente de MySQL de línea de comandos, indicando la cadena de conexión y el usuario que hemos definido como administrador. En el parámetro host `-h` ponemos el nombre del servidor (endpoint que hemos copiado en el portapapeles) y en el parámetro de usuario `-u` el nombre del usuario. Para que nos solicite el password indicamos el parámetro `-p`.

`mysql -h database-jrpm.cruqs8qiedha.us-east-1.rds.amazonaws.com -u admin -p`

Una vez comprobada la conexión, cerramos la sesión:

`exit;`

!!! warning "Atención"

    Si hemos dejado la opción de **Permitir Acceso Público** como **NO** o no aparece la regla de seguridad del firewall (grupo de seguridad) no podremos conectarnos.

3.- Vamos a crear una base de datos con una tabla. Lo vamos a hacer mediante un script de sentencias sql. Para ello comenzamos con la descarga del fichero de creación de la base de datos.

[Descarga fichero sql](../ud05/asir.sql)

4.- Ejecutamos las instrucciones SQL que hay en el contenido del fichero descargado. Basta con redireccionar la entrada del comando `mysql` con el fichero descargado de nombre `asir.sql`.

```
mysql -h database-jrpm.cruqs8qiedha.us-east-1.rds.amazonaws.com -u admin -p < asir.sql
```

<br>
___

### Estresando la BBDD

5.- Vamos a simular varias conexiones simultáneas a nuestra base de datos mediante el programa `mysqlslap` que es una herramienta que viene instalada con el cliente de MySQL. Para ello ejecutamos el siguiente comando:

```
mysqlslap -h <endpoint>> -u admin -p \
--concurrency=50 --iterations=10 \
--number-of-queries=1000 \
--create-schema=webasir --query="SELECT * FROM clientes;"
```

El comando simula 50 conexiones simultáneas que ejecutan 1000 veces el query indicado.

<br>
___

### Monitorización desde Cloudwatch

6.- Accede al servicio **CloudWatch**:

- En el panel lateral accede al menú **Paneles** --> **Crear Panel**
- Dale un nombre: *BasedeDatos*
- Comienza añadiendo un widget de métrica de tipo **Línea**
- De las métricas disponibles selecciona las de **RDS**.
- Pulsa sobre **DBinstanceIdentifier**.
- Selcciona la métrica *DataBaseConnections*.
- Una vez añadido el widget, pulsa sobre el botón **+** y añade varios más:
    - *ReadIOPS*
    - *WriteIOPS*
    - *ReadLatency*
    - *CPUUtilization*
    - *FreeStorageSpace* (widget tipo Número)



!!! success "Captura la pantalla"
    Captura la pantalla en la que se vea el panel creado con varios widgets. Interpreta el significado de cada métrica mostrada.

<br>
___

### Eliminación de los recursos creados

7.- Desde la consola de AWS, **elimina el servidor de BBDD creado para asegurarnos que no dejamos ningún recurso consumiendo crédito**. No crees ninguna instantánea final ni conserves las copias de seguridad.

!!! warning "Atención"
    Si detenemos un servidor de BBDD (sin eliminarlo), AWS lo iniciará automáticamente a los 7 días (si no lo hemos levantado nosotros de manera manual antes). Esto es peligroso, pues si olvidamos eliminar un recurso de BBDD que no utilizamos, se pondrá en marcha automáticamente a los 7 días de haberlo detenido, con el consiguiente consumo de crédito.

<img src="../images/ud05/BBDD_03.png" width=400>