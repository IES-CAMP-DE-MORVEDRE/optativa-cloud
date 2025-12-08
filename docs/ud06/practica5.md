# Práctica 5. Función Lambda con API Gateway

Creación de una función Lambda que recibe parámetros en formato json meidante la llamada a una API Gateway.

## Objetivo de la práctica

* Crear una fnción Lambda desde cero que trabaje con parámetros recibidos.
* Crear un API Gateway como desencadenador.
* Llamar a la función desde una máquina remota utilizando la llamada a la API.
* Comprobación de los resultados devueltos por la función.

!!!example "Descarga del software necesario"
    Para probar el funcionamiento de la API es recomendable utilizar algún software para depurar y probar APIs como puede ser **Insomnia**, **Postman** u otros similares. Puedes descargar **Insomnia** en [https://insomnia.rest/](https://insomnia.rest/) válido para Windows, Linux y Mac.

## Práctica a realizar

### Modificación del código

1.- Vamos a utilizar la función Lambda creada en la práctica anterior, pero vamos a modificar ligeramente el código para obtener los parámetros, pues la forma de recibirlos cambiará al utilizar el API Gateway.

```python
import json

def lambda_handler(event, context):
    # Imprimimos en la consola de logs el event recibido
    print("Event recibido: " + json.dumps(event, indent=2))

    # Recuperamos los parámetros recibidos y los almacenamos en variables
    nombre = event['queryStringParameters']['key1']
    apellido1 = event['queryStringParameters']['key2']
    apellido2 = event['queryStringParameters']['key3']

    # Imprimimos en la consola de logs los 3 parámetros recibidos
    print("Nombre = " + nombre)
    print("Apellido 1 = " + apellido1)
    print("Apellido 2 = " + apellido2)

    # Construimos el valor a devolver como resultado de concatenarlos
    resultado = f"{apellido1} {apellido2}, {nombre}"

    # Devolvemos el string
    return resultado
```

---

2.- Haz un **Deploy**

### Creación del desencadenador

3.- En el **Diagrama** pulsa sobre **Agregar desecandenador**.

- En la configuración del desencadenador eleccionamos el origen **API Gateway**:
    - Crear una **API Nueva**.
    - Tipo de API: **API HTTP**.
    - Seguridad: **Abrir**.

Esto nos ha creado un nuevo servicio de **API Gateway** que podemos configurar sus rutas, permisos, controlar los logs, etc. No vamos a tocar nada.

---

### Comprobación del endpoint

4.- Ve a la pestaña **Configurar** y accede a la opción **Desencadenadores**,o pulsa directamente sobre **API Gateway** del Diagrama.

5.- Copia el endpoint (punto de enlace) que aparece asociado a la API.

---

### Ejecución de la API

6.- Abre el programa **Insomnia**.

7.- Pega la url del endpoint junto al comando GET que aparece. Si pulsáramos sobre el botón **Send** para invocar a la API nos devolvería un error puesto que nuestra función está esperando unos parámetros que no le hemos pasado.

8.- En el apartado de **Query Parameters** asigna 3 nuevos parámetros que se llamen como los que espera la función: `key1`, `key2`, `key3`. Sus valores serán tu nombre, apellido1 y apellido2 respectivamente.

9.- Pulsa ahora sobre el botón **Send** y comprueba que se ha ejecutado bien y el valor devuelto es el esperado.


!!!success "Captura la pantalla"
    Captura la pantalla de Insomnia en la que se vea el paso de los parámetros y el resultado devuelto por la función.