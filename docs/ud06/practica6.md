# Práctica 6. Función Lambda con API Gateway y DynamoDB

Creación de una API que hace operaciones de lectura y escritura en una Base de Datos DynamoDB.

## Objetivo de la práctica

* Crear una fnción Lambda que trabaje con parámetros recibidos y actúe sobre una base de datos.
* Crear un API Gateway como desencadenador.
* Llamar a la función desde una máquina remota utilizando la llamada a la API.
* Hacer operaciones de lectura y escritura en una BBDD DynamoDB

## Práctica a realizar

### Creación de la Base de Datos

1.- Accedemos al servicio **DynamoDB** y **Creamos una tabla**:

- El nombre de la tabla: **meteo**
- Clave de partición: **sensor** de tipo *cadena*
- Clave de ordenación: **timestamp** de tipo *cadena*

2.- Una vez creada la tabla, accedemos a ella y pulsamos sobre **Explorar elementos**.

3.- Vamos a añadir elementos de forma manual a la tabla. Para ello pulsamos sobre **crear elementos** e introducimos los siguientes elementos (agregando los atributos *temperatura* y *humedad*, ambos como tipo numérico):

| sensor (cadena) | timestamp (cadena)        | temperatura (número) | humedad (número) |
|-----------------|---------------------------|----------------------|------------------|
| sensor01        | 2025-12-12T12:00:00+01:00 | 23.7                 | 75               |
| sensor02        | 2025-12-12T12:00:00+01:00 | 24.1                 | 76               |
| sensor01        | 2025-12-12T12:05:00+01:00 | 23.8                 | 74               |

Se pueden introducir los valores mediante cadenas json. El equivalente del primer registro sería lo siguiente:

```json
{
  "sensor": {
    "S": "sensor01"
  },
  "timestamp": {
    "S": "2025-12-12T12:00:00+01:00"
  },
  "temperatura": {
    "N": "23.7"
  },
  "humedad": {
    "N": "75"
  }
}
```

---

### Creación de la función

4.- **Crea una nueva función Lambda**, pero esta vez vamos a usar una plantilla predefinida. Para ello, pulsa sobre **Usar un esquema**.

- El esquema a utilizar será **Create a microservice that interacts with a DDB table** usando como lenguaje **python 3.12**
- Asigna un nombre de función que contenga tus iniciales.
- El Rol de ejecución será **LabRole**.
- Deja el código sin modificar nada.
- Como desencadenador de API Gateway selecciona **Crear una API nueva**:
    - El tipo de API selecciona **API de REST** (la última).
    - Seguridad: **Abrir**

!!!note "REST APIs vs HTTP APIs"
    En esta ocasión vamos a utilizar un API Gateway de tipo REST API, que es más completo que la HTTP API. Está basada en la arquitectura RESTful y funciona con métodos HTTP estándar: GET, POST, PUT, DELETE. 

---

### Despliegue de la función

5.- Vamos a dejar íntegramente el código que nos propone por defecto, sin modificar absolutamente nada. Este sencillo código está optimizado para extraer el cuerpo del evento que recibe, y en base al método que se le especifique en la llamada de la API (GET, POST, DELETE, PUT) hacer una operación u otra sobre la tabla DynamoDB que se le pase.

6.- Haz un **Deploy** (no es necesario).

---

### Visualización del endpoint de la API

7.- Accede al API Gateway y copia la url del endpoint.

---

### Ejecución de la API mediante el método GET

Vamos a hacer una consulta a la tabla DynamoDB mediante la invocación de nuestra función Lambda. Para ello, hay que pasarle al código de la función que vamos a utilizar el método GET y como parámetro el nombre de la tabla DynamoDb que hemos creado y sobre la que queremos hacer la consulta.

8.- Abre el programa **Insomnia**.

9.- Pega la url del endpoint junto al comando **GET** que aparece.

10.- En el apartado de **Parameters** pon el siguiente parámetro:
    
- name: **TableName**
- value: **meteo** (nombre de la tabla DynamoDB)

11.- Pulsa ahora sobre el botón **Send** y comprueba que se ha ejecutado la API y nos devuelve todos los valores introducidos en la tabla.

---

### Ejecución de la API mediante el método POST

Vamos a hacer una inserción de elemento a la tabla DynamoDB mediante la invocación de nuestra función Lambda. Para ello, hay que pasarle al código de la función que vamos a utilizar el método POST y en el cuerpo (*body*) del evento el nombre de la tabla DynamoDb que hemos creado y los datos del elemento que queremos insertar en formato json.

12.- Selecciona ahora como método de invocación el método **POST**

13.- En el apartado de **Parameters** déjalo en blanco, elimina el valor introducido anteriormente.

14.- En el apartado **Body** selecciona que vamos a intriducir los datos en formato **json** y pega el siguiente código que contiene el elemento a insertar y el nombre de la tabla:

```json
{
  "TableName": "meteo",
  "Item": {
    "sensor": { "S": "sensor01" },
    "temperatura": { "N": "24.9" },
    "humedad": { "N": "78" },
    "timestamp": { "S": "2025-12-12T12:10:00+01:00" }
  }
}
```

15.- Envía el método POST a nuestra API.

!!!success "Captura la pantalla"
    Captura la pantalla de Insomnia en la que se vea el *body* y el status `200 OK` devuelto por la función después de insertar el elemento en la tabla de DynamoDB.