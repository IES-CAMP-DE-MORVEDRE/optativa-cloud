# Práctica 4. Función Lambda con parámetros

Creación de una función Lambda que recibe parámetros en formato json.

## Objetivo de la práctica

* Crear una fnción Lambda desde cero que trabaje con parámetros recibidos.
* Paso de parámetros a la función durante la llamada.
* Comprobación de los logs de ejecución.

## Práctica a realizar

### Creación de la función

1.- Crea una nueva función Lambda **desde cero**.

- Asigna un nombre de función que contenga tus iniciales.
- El lenguaje de programación será **Python 3.14**
- El Rol de ejecución será **LabRole**.
- Deja los demás valores por defecto.

---

### Modificación del código de la función

2.- Vamos a modificar el código que nos propone por defecto por el siguiente:

```python
import json

def lambda_handler(event, context):
    # Imprimimos en la consola de logs el event recibido
    print("Event recibido: " + json.dumps(event, indent=2))

    # Recuperamos los parámetros recibidos y los almacenamos en variables
    nombre = event['key1']
    apellido1 = event['key2']
    apellido2 = event['key3']

    # Imprimimos en la consola de logs los 3 parámetros recibidos
    print("Nombre = " + nombre)
    print("Apellido 1 = " + apellido1)
    print("Apellido 2 = " + apellido2)

    # Construimos el valor a devolver como resultado de concatenarlos
    resultado = f"{apellido1} {apellido2}, {nombre}"

    # Devolvemos el string
    return resultado
```

Esta función imprime por la consola de logs los tres parámetros recibidos y devuelve mediante el comando `return` un nuevo campo con los 3 parámetros combinados. 

3.- Haz un **Deploy** del código para que esté lista la función para ser invocada.

---

### Prueba de la función

4.- Ve a la pestaña **Probar** y crea un evento de prueba:

- Pon el nombre que quieras.
- Utiliza la plantilla de *Hello World*

>Esta plantilla de test crea 3 parámetros llamados `key1`, `key2` y `key3` dentro de una cadena json.

5.- Sustituye los valores por tu Nombre, Apellido 1 y Apellido 2.

6.- Pulsa sobre **Probar**.

### Comprobación de los logs

7.- Ve a la pestaña de **Monitorear** de la función lambda.

8.- Pulsa sobre **Ver registros en CloudWatch**.

!!!success "Captura la pantalla"
    Captura la pantalla en la que se vean los mensajes que hemos mandado por la consola con `print` (objeto event y parámetros) al ejecutar la función con el evento de prueba.