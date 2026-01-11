# Práctica 3. Logs en CloudWacth

Visualización de logs en CloudWacth

## Objetivo de la práctica

* Visualizar logs generados automáticamente por las funciones Lambda.
* Identificar Log Groups (Grupos de Registro) y Log Streams (Flujos de Registro) asociados a una función Lambda.
* Interpretar la información básica de los logs (START, END, REPORT).
* Consultar logs usando CloudWatch Logs Insights.

!!! warning "Atención"
    CloudWatch puede recibir logs de muchos servicios de AWS, pero **no todos lo hacen automáticamente**. Servicios como **AWS Lambda, API Gateway o Step Functions** envían sus logs a CloudWatch de forma automática, sin necesidad de instalar agentes ni realizar configuraciones adicionales. En estos casos, AWS crea por sí mismo los *Log Groups* y *Log Streams*, y los logs aparecen en CloudWatch en cuanto el servicio se ejecuta.

    Otros servicios, como **EC2, contenedores o aplicaciones propias**, requieren una **configuración explícita** para enviar logs. Esto implica asignar **permisos IAM adecuados** y, normalmente, instalar y configurar el **CloudWatch Agent** o usar el SDK de AWS. En todos los casos, para que existan logs es imprescindible que haya un **origen que los genere**, permisos para enviarlos y un **destino en CloudWatch** donde almacenarlos.


## Requisitos previos

Es necesario haber realizado alguna práctica de la *Unidad 6: Microservicios y arquitecturas sin servidor* y no haber borrado los logs de la ejecución de las funciones Lambda.

## Práctica a realizar

### Acceso a los Grupos de Registro

1.- Accede al servicio **CloudWatch**:

- En el panel lateral accede al menú **Registros** --> **Log Management**
- Nos aparecen los **Grupos de Registro** (*Log Groups*)
- Busca un Log Group con el formato: `/aws/lambda/nombre-de-la-funcion`
- Este Log Group:
    - Se crea automáticamente
    - Tiene el mismo nombre que la función
- Haz clic sobre él.

<br>

---

### Explorar los Flujos de Registro

Dentro del Grupo de Registros pueden aparecer varios **Flujos de Registro** (*Log Streams*). Cada uno corresponde a:

- Una ejecución
- O a un contenedor reutilizado por Lambda

El nombre suele incluir:

- Fecha
- Identificador único

2.- Selecciona uno de ellos.

<br>

---

### Interpretar los logs de una ejecución

Al abrir un Log Stream típico veremos los **Eventos de Registro**, algo parecido a esto:

```
START RequestId: xxx Version: $LATEST
```
```
Mensaje generado por la función
```
```
END RequestId: xxx
```
```
REPORT RequestId: xxx Duration: 3.45 ms Billed Duration: 4 ms Memory Size: 128 MB Max Memory Used: 57 MB
```

Cada uno de estos eventos tiene una información relacionada con distintos eventos de la función que se ha ejecutado.

- START
    - Inicio de la ejecución de la función.
- Mensajes intermedios
    - Salidas del código (por ejemplo `console.log`, `print`, etc.).
- END
    - Fin de la ejecución.
- REPORT
    - Información de rendimiento (esta línea es clave para optimización y costes):
        - Tiempo de ejecución
        - Memoria asignada
        - Memoria utilizada


!!! success "Captura la pantalla"
    Captura la pantalla en la que se vea los eventos de registro de un flujo de registro en concreto.

<br>

---

### Consultas con Logs Insights

**CloudWatch Logs Insights** es una herramienta de AWS que permite **buscar, filtrar y analizar de forma rápida los logs almacenados en CloudWatch**, usando un lenguaje de consultas sencillo. Facilita encontrar errores, analizar ejecuciones y obtener estadísticas sin necesidad de descargar los logs.

Utiliza un lenguaje de consultas propio de AWS, específico para el análisis de logs. Es un lenguaje declarativo y orientado a búsquedas, inspirado en SQL pero **no es SQL estándar**, diseñado para filtrar, ordenar y obtener estadísticas a partir de registros de texto de forma eficiente.

3.- En el panel lateral del servicio **CloudWatch** accede al menú **Registros** --> **Logs Insights**:

- Selecciona un grupo de registro de los asociados a la ejecución de las funciones lambda que tenías.
- Especifica un rango de tiempo (por defecto aparece seleccionado una hora) que incluya la fecha de la ejecución de la función lambda.
- Deja el query que viene por defecto:
```
fields @timestamp, @message
| sort @timestamp desc
| limit 10000
```
- Ejecuta la consulta.

Deben aparecer los eventos de registro asociados al grupo de registros seleccionados ordenados por fecha más reciente.

Prueba a cambiar la consulta:

- Logs en los que aparece la palabra "error":
```
fields @timestamp, @message
| filter @message =~ /error/
| sort @timestamp desc
```
- Ver duración de las ejecuciones de la función lambda:
```
filter @type = "REPORT"
| stats avg(@duration), max(@duration)
```


!!! success "Captura la pantalla"
    Captura la pantalla en la que se vea la ejcución satisfactoria de alguna consulta.