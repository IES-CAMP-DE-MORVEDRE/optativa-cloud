# Práctica 2. Función Lambda con url de activación

Creación  de una función Lambda y activación mediante la invocación de una url

## Objetivo de la práctica

* Crear una fnción Lambda desde cero.
* Activación de la función desde una url.
* Comprobación de los logs de ejecución.

## Práctica a realizar

### Creación de la función

1.- crea una nueva función Lambda **desde cero**.

- Asigna un nombre de función que contenga tus iniciales.
- El lenguaje de programación será **Python 3.14**
- El Rol de ejecución será **LabRole**.
- Deja los demás valores por defecto.
> Podríamos asignar una url de activación desde el apartado **Configuraciones adicionales** pero lo vamos a hacer una vez creada la función.

---

### Modificación del código de la función

2.- Vamos a dejar el código que nos propone por defecto pero modificando el mensaje de retorno de `"Hello from Lambda!"` por uno en el que aparezca tu nombre.

```python
import json

def lambda_handler(event, context):
    # TODO implement
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }
```

Esta función únicamente devuelve un valor mediante el comando `return`. El valor que devuelve es un dicionario Python que contiene 2 claves:

- `satusCode`: Un valor en el que se le puede indicar al evento que invocó la función un código de finalización de correcto o con error.
- `body`: Un cuerpo que en este caso devuelve un texto (`Hello from Lambda!`) en formato json.

3.- Haz un **Deploy** del código para que esté lista la función para ser invocada.

---

### Creación de una url de función

4.- Ve a la pestaña de configuración.

5.- En el menú del panel lateral accede a **URL de la función**.

6.- Crea una nueva url de función:

- El tipo de auorización será **NONE**.
- Los demás campos por defecto.

### Ejecución de la función

7.- Una vez creada la url asociada a la función, ábrela en un navegador y verás que se ejecuta y te muestra la respuesta devuelta por la función en el comando `return`.

8.- Si refrescas el navegador o vuelves a pinchar en el enlace, se volverá a ejecutar la función.

!!!success "Captura la pantalla"
    Captura la pantalla en la que se vea en el navegador la url y el mensaje devuelto por tu función.

### Comprobación de los logs

9.- Ve a la pestaña de **Monitorear** de la función lambda.

10.- Pulsa sobre **Ver registros en CloudWatch**.

11.- Te aparecerá un Flujo de registros por cada vez que se modifique la función. Si entramos a examinarlos veremos que aparecen los logs de cada una de las veces que se ha ejecutado la función Lambda. 

!!!note "Nota"
    Si hubiéramos puesto algún comando `print` en la función, podríamos ver su salida en estos logs.