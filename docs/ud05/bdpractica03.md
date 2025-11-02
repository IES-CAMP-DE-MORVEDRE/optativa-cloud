# Despliegue de un Clúster de Aurora

## Objetivo de la práctica

Vamos a crear un clúster de BBDD con Aurora en el que tendremos varias instancias: una primaria (escritora) y una o varias secundarias (lectoras). Esto nos dará una **alta disponibilidad** y un **alto rendimiento**.

- **Alta disponibilidad**: Al tener varias instancias y el almacenamiento compartido, implica que si uno de los nodos falla (incluso el principal) los demás siguen funcionando y dando servicio.
- **Alto rendimiento**: Al trabajar con varias instancias lectoras, las cargas de trabajo de las operaciones de lectura sobre la base de datos se reparte entre todas las instancias, trabajando en paralelo y mejorando el rendimiento.

### Elementos principales de un clúster Aurora

**1.- Almacenamiento compartido (Cluster Volume)**

- Los datos no se guardan en cada instancia de la base de datos, sino en un volumen distribuido y replicado automáticamente en 3 AZs distintas dentro de la región.
- Esto da alta disponibilidad y durabilidad (copias redundantes).

**2.- Instancia primaria (Writer)**

- Es la que puede escribir en la base de datos.
- Maneja todas las operaciones de lectura y escritura.

**3.- Instancias de solo lectura (Readers)**

- Opcionales, pero muy útiles.
- Solo aceptan lecturas, y puedes añadir varias para escalar el rendimiento.
- El tráfico de lectura se reparte con un endpoint de lecturas.

**4.- Endpoints del clúster**

- **Cluster endpoint** (writer endpoint): apunta siempre a la instancia primaria.
- **Reader endpoint**: balancea las conexiones entre las réplicas de lectura.

<img src="../images/ud05/practica3/aurora01.png" width=700>

## Práctica a realizar

### Creación de la Base de Datos Aurora

1.-  Accedemos a la consola, dentro de la categoría Bases de Datos, seleccionamos el recurso **Aurora and RDS**.

!!! note "Nota"
    Aurora permite hasta 2 motores de BBDD distintos: MySQL y PostgrSQL. En esta práctica, utilizaremos el **compatible con MySQL**.

<br>
___

2.-	Creamos una Base de Datos:

- Seleccionamos el método de *creación estándar*.
- Como motor de base de datos elegimos **Aurora (MySQL Compatible)**.
- La plantilla sobre la que se va a basar será **Desarrollo y pruebas** (las demás no son aptas para el laboratorio).
- Ponemos un nombre de servidor que debe ser único en nuestra cuenta de AWS. Introduce uno que lleve tu nombre o iniciales.
- Asignamos nombre de usuario administrador y su contraseña (**Credenciales Autoadministrado**).
- El Almacenamiento del clúster lo configuramos como **Aurora Estándar**.
- En la configuración de la instancia seleccionamos **Clases ampliables (incluye calses t)**, pues con el de *Clases optimizadas para memoria* no tendremos permisos de creación en el laboratorio.

!!! note "Serverless"
    La opción de crear un cluster **Sin servidor** (*Serverless*) sería apropiada para los siguientes casos:

    - Aplicaciones con carga variable o impredecible.
    - Entornos de desarrollo o testing, donde la base de datos no está en uso todo el tiempo.
    - APIs y microservicios que no necesitan una base de datos activa 24/7.

    Esta práctica entraría en uno de estos casos, pero en el laboratorio **no tenemos permisos** para crear este tipo de clústers.


- Elegimos un tamaño de instancia **db.t3.medium**.
- En disponibilidad y durabilidad seleccionamos la opción de **creación de un nodo de lectura en una AZ diferente**. De esta manera, haremos un despliegue MultiAZ. Tendremos una instancia de lectura en otra zona de disponibilidad (AZ), lo cual nos permite tener alta disponibilidad y una conmutación por error alta. Es decir, si falla la instancia principal, esta réplica ocupará su lugar en un tiempo reducido.
- Por simplificar, en conectividad selecionamos que **No se conecte a una EC2**. Ya sabemos que esto no es lo recomendable, pues no es seguro dejar expuesto el accedo a la base de datos desde Internet.
- Activamos la opción **Sí de Acceso Público** (insistimos en la peligrosidad de esta opción) y le ponemos nombre al nuevo grupo de seguridad: **grupo-seguridad-acceso-aurora**
- Desactivamos la **Monitorización mejorada** (por tema de permisos también).
- Creamos la base de datos.
- Ignoramos el mensaje de instalar Complementos sugeridos y esperamos a que se cree nuestro clúster Aurora.


!!! warning "Atención"
    Cuando hemos creado el grupo de seguridad, si no modificamos nada, por defecto AWS permite el acceso a la BBDD desde una **única IP**. Esto es importante tenerlo en cuenta. Si luego intentamos acceder desde otro equipo, o desde el mismo pero en otra red **(cambia nuestra IP Pública)**, no podremos conectarnos.

<br>
___

### Comprobación del clúster

2.-  Una vez creado el clúster, comprobamos que se nos ha creado con 2 nodos (uno pricipal, **escritor**) y uno secundario (**la réplica lectora**).

- Accedemos al clúster y vemos que se nos han creado varios **endpoints**:

    - Dos endpoints al clúster:
        
        - Writer Endpoint: Apunta siempre a la instancia primaria.
        - Reader Endpoint: balancea las conexiones entre las réplicas de lectura.

    - Dos endpoints, uno por cada instancia:

        - Endpoint a la instancia escritora.
        - Endpoint a la instancia lectora.

!!! tip
    Lo normal será acceder a los **endpoints del cluster**, y no al de una instancia en concreto. 
    
    Utilizaremos el **Writer endpoint** del clúster para operaciones de escritura y el **Reader endpoint** del clúster para operaciones de lectura, sin importarnos en qué instancia accederemos.

<img src="../images/ud05/practica3/aurora02.png">

<br>
___

### Acceso a la Base de Datos

3.- Copia el endpoint escritor del cluster y accede a él desde tu máquina local mediante `mysql`.

```
mysql -h database-jrpm.cluster-c5gac0s6ydn6.us-east-1.rds.amazonaws.com -u admin -p
```

Comprueba que puedes crear una base de datos:

```
create database pruebas;
```

4.- Cierra la sesión y conéctate ahora utilizando el **endpoint de lectura**.

- Conéctate al clúster para operación de lecturas.
- Teclea `use pruebas;` y comprueba que podemos acceder sin problemas a la BBDD creada anteriormente.
- Prueba a crear una nueva BBDD usando el comando `create database`.

!!! success "Captura las pantallas"
    Captura la pantalla en la que se vea la **conexión al endpoint de lecturas**, el** acceso a la BBDD `pruebas`** creada y el **error al intentar crear** una nueva BBDD.


<br>
___

### Escalado del clúster

Sabemos que hay 2 tipos de escalado para las instancias en general: **Vertical** y **Horizontal**. En Aurora podemos escalar del mismo modo:

- **Escalado Vertical**: consiste en incrementar o decrementar la “potencia” de la instancia (de la máquina). Para escalar verticalmente una instancia de Amazon Aurora, tendríamos que seleccionarla y pulsar el botón Modificar. En la clase instancia seleccionaríamos una de mayor (o de menor) capacidad.
- **Escalado Horizontal**: consiste en incrementar o decrementar el número de réplicas de lectura. Con un aumento de las instancias, conseguiríamos una menor latencia debido al balanceo de la carga.

5.- Vamos a añadir una réplica de lectura a nuestro clúster (escalado horizontal). Seleccionamos el clúster y en **Acciones** pulsamos sobre **Agregar lector**.

- Le ponemos un nombre y dejamos todas las demás opciones con su valor por defecto.

Una vez creado el nuevo nodo (le cuesta unos minutos), veremos que nuestro clúster tiene una nueva instancia lectora sobre la que balancear las cargas de peticiones de lectura.

!!! success "Captura las pantallas"
    Captura la pantalla en la que se vea el nuevo nodo de lectura en el clúster.

<br>
___

### Eliminación de los recursos creados

Para finalizar la práctica eliminamos los recursos creados.

!!! danger "Peligro"
    Este servicio consume mucho crédito. Asegúrate de eliminarlo, pues incluso con el laboratorio apagado y la BBDD parada, sigue consumiendo crédito.

8- Desde la consola de AWS, **elimina el servidor de BBDD creado para asegurarnos que no dejamos ningún recurso consumiendo crédito**. 

!!! warning "Atención"
    Para eliminar la BBDD hay que eliminar primero las instancias que componen el clúster.

!!! info
    Podemos optar por resetear el laboratorio (proceso costoso, pero sólo hay que darle a un botón). Este proceso deja el laboratorio "de fábrica" pero no nos restablece el saldo.




