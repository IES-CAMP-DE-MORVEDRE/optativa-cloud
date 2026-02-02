# Proyecto ASIR 2ª Evaluación: <br> Despliegue de una Web y Base de Datos Altamente Disponible


## 1. Contexto del proyecto

Nuestra empresa desea implantar una aplicación web cuyo objetivo principal será consultar información almacenada en una base de datos central. La web actuará únicamente como visor, mientras que la incorporación de nuevos datos se realizará a través de un servicio independiente, preparado para recibir información desde distintos sistemas y garantizar un funcionamiento seguro y ordenado. Este planteamiento permitirá que la solución crezca en el futuro sin complicar el uso de la aplicación web.

Debido al carácter crítico de los datos que se manejan, nuestra empresa desea que los datos estén siempre accesibles desde la web, sin permitir ni un solo minuto de pérdida de servicio, y con tiempos de respuesta aceptables independientemente de la carga de trabajo, que es imprevisible.

## 2. Objetivo general

Como administradores de sistemas queremos desplegar y gestionar una infraestructura en AWS que aloje una aplicación web en PHP conectada a una base de datos **para garantizar alta disponibilidad, escalabilidad automática y seguridad en el acceso a los datos**.

## 3. Requisitos funcionales

Diseñar e implementar una arquitectura en AWS que permita:

- Alojar una **página web en PHP** capaz de leer datos desde una base de datos y mostrar elementos multimedia alojados en un bucket S3.
- Exponer una **API REST** que permita insertar datos en la base de datos.
- Garantizar **alta disponibilidad** tanto en la capa web como en la capa de datos.
- Garantizar **autoescalado** en la capa web para evitar pérdidas de rendimiento en la experiencia de usuario.
- Aplicar medidas de **seguridad** adecuadas en todos los niveles de la infraestructura.

### 3.1 Aplicación web

- La aplicación web deberá estar desarrollada en **PHP**.
- La web deberá **consultar y mostrar** los datos almacenados en la base de datos.
- No se permitirá la inserción directa de datos en la base de datos desde la web.
- Las imágenes y elementos multimedia de la página web los debe recuperar de un **bucket S3**.

### 3.2 API de inserción de datos

- Se deberá desarrollar una **API REST** utilizando **AWS Lambda**.
- La API deberá recibir datos mediante peticiones HTTP (por ejemplo, `POST`).
- La función Lambda será la encargada de **insertar los datos** en la base de datos.
- Los parámetros de conexión a la BBDD se almacenarán en variables de entorno.

### 3.3 Base de datos

- La base de datos deberá ser una **base de datos relacional** y **altamente disponible**.
- Deberá permitir la creación de **réplicas de lectura** para mejorar el rendimiento.
- Se utilizará al menos una **tabla** para almacenar la información recibida por la API.

## 4. Requisitos no funcionales

### 4.1 Alta disponibilidad y escalabilidad

- La infraestructura de la web deberá ser **altamente disponible**, distribuyéndose en al menos **dos zonas de disponibilidad**.
- La capa web deberá ser **autoescalable**, adaptándose automáticamente a la carga.
- La base de datos deberá tolerar fallos sin pérdida de servicio.
- La base de datos podrá ser escalable de manera manual.

### 4.2 Seguridad

- No se permitirá el acceso público directo a la base de datos.
- Se deberán utilizar **grupos de seguridad** siguiendo el principio de mínimo privilegio.
- Las comunicaciones entre los distintos componentes deberán realizarse de forma segura.

### 4.3 Mantenimiento y buenas prácticas

- Se deberán utilizar servicios gestionados siempre que sea posible.
- La arquitectura deberá ser fácilmente ampliable y mantenible.
- Se valorará el uso de mecanismos de monitorización y registro de logs.

## 5. Alcance del proyecto

El proyecto incluirá:

- Diseño de la **arquitectura AWS**.
- Creación de la infraestructura necesaria.
- Desarrollo básico de la aplicación web en PHP.
- Desarrollo de la función **Lambda** y la API asociada.
- Configuración de la base de datos y sus réplicas de lectura.
- Aplicación de medidas de seguridad.

## 6. Entregables

Para la evaluación se deberá entregar:

- Un **documento descriptivo de la arquitectura**, incluyendo un diagrama.
- Justificación de los servicios AWS utilizados.
- Código fuente de la aplicación web y de la función Lambda.
- Explicación de las medidas de seguridad implementadas.
- Breve guía de despliegue y funcionamiento de la solución.

## 7. Criterios de evaluación

Se valorará especialmente:

- Correcta implementación de la **alta disponibilidad** y el **autoescalado**.
- Uso adecuado de servicios AWS.
- Seguridad de la arquitectura.
- Funcionamiento correcto de la web y la API.
- Uso de mecanismos de monitorización y registro de logs.
- Claridad y calidad de la documentación entregada.

