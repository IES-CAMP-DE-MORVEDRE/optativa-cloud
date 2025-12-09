# Práctica 3. Función Lambda con desencadenador

Creación de una función Lambda y activación mediante un desencadenador.

## Objetivo de la práctica

* Crear un desencadenador para una función lambda para que se ejeucte cada minuto.
* Comprobación de la ejecución automática de la función.

!!!note "Desencadenadores"
    Un desencadenador Lambda (o *trigger*) es un evento o servicio de AWS que automáticamente invoca una función Lambda para ejecutar su código. Este evento pueder ser una petición HTTP, una subida a S3, o un cambio en una base de datos DynamoDB o incluso una programación de *cron* o planificación temporal.

## Práctica a realizar

### Creación del desencadenador

1.- Vamos a utilizar la función Lambda creada en la práctica anterior. Accede a ella y en el **Diagrama** pulsa sobre **Agregar desecandenador**.

- En la configuración del desencadenador eleccionamos el origen **EventBridge (ColudWatch Events)**
- Creamos una **nueva regla**:
    - Nombre: *CadaMinuto*
    - Descripción: *Evento a ejecutar cada minuto.*
    - Expresión de programación: `rate(1 minute)`

!!!info
    En la expresión de programación se pueden utilizar expresiones de cron o expresiones de frecuencia (*rate expression*). Consulta la [documentación](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-scheduled-rule-pattern.html) para ver cómo utilizarla.

A partir de este momento la función ya se ejecutará automáticamente cada minuto.

<br>

---

### Comprobación de los logs

2.- Accede a los registros de **CloudWatch** para comprobar que la función se está ejecutando cada minuto.


!!!success "Captura la pantalla"
    Captura la pantalla en la que se vea en el diagrama de la función que se ha añadido un desencadenador de EventBridge.

<br>

---

### Eliminación del desencadenador

3.- Para evitar que la función esté continuamente ejecutándose, accede a la pestaña de **Configuración** y en el panel lateral accede a **Desencadenadores**

4.- Elimina el desencadenador.

!!!warning "Atención"
    Es posible que no nos deje eliminar el desencadenador o que tras eliminarlo siga apareciendo en la consola. Es necesario elimnar también un permiso (Panel lateral --> **Permisos**) asociado a una entidad principal llamada *events.amazonaws.com* para que deje de aparecer el desencadenador.