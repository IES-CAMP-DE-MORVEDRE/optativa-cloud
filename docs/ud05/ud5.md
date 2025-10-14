# Introducción a Bases de Datos en AWS

## 1. Introducción general

Las **bases de datos** son el corazón de casi cualquier aplicación moderna. Permiten almacenar, organizar y recuperar información de forma estructurada y segura.
En el entorno de **Amazon Web Services (AWS)**, existen diferentes opciones que se adaptan a las necesidades de cada caso: desde sistemas **relacionales tradicionales** hasta soluciones **NoSQL** diseñadas para grandes volúmenes de datos no estructurados.

---

## 2. Tipos de bases de datos

### 2.1 Bases de datos relacionales (SQL)

Las bases de datos relacionales organizan la información en **tablas** compuestas por filas y columnas, donde los datos se relacionan entre sí mediante **claves primarias y foráneas**.
En AWS, el servicio que gestiona este tipo de bases de datos es **Amazon RDS (Relational Database Service)**.

#### Principales motores disponibles en RDS:

| Motor                                | Características                                                      | Casos de uso                                             |
| ------------------------------------ | --------------------------------------------------------------------- | -------------------------------------------------------- |
| **MariaDB**                    | Open source, compatible con MySQL, alto rendimiento                   | Aplicaciones web, CMS como WordPress                     |
| **MySQL**                      | Amplio soporte y comunidad, ideal para proyectos pequeños y medianos | Aplicaciones de comercio electrónico o SaaS             |
| **PostgreSQL**                 | Robusto, con soporte para JSON, funciones avanzadas                   | Aplicaciones empresariales y analíticas                 |
| **Amazon Aurora**              | Compatible con MySQL y PostgreSQL, optimizado por AWS                 | Aplicaciones críticas que requieren alta disponibilidad |
| **Otros (Oracle, SQL Server)** | Integración empresarial, soporte para procedimientos almacenados     | ERP, CRM, entornos corporativos                          |

#### Ventajas de usar RDS:

- Administración automática de parches, copias de seguridad y actualizaciones.
- Escalado vertical u horizontal según demanda.
- Alta disponibilidad mediante réplicas Multi-AZ.
- Integración con otras herramientas de AWS (CloudWatch, IAM, VPC).

---

### 2.2 Bases de datos NoSQL

Cuando los datos no siguen un esquema fijo (por ejemplo, registros de usuarios, logs o catálogos de productos con diferentes atributos), las bases **NoSQL** ofrecen mayor flexibilidad y rendimiento.

#### Amazon DynamoDB

- Base de datos **NoSQL totalmente gestionada**.
- Almacena datos en formato **clave-valor** o **documento**.
- Escala automáticamente en función de la carga.
- Latencia baja (milisegundos) ideal para aplicaciones móviles o IoT.

**Ejemplo de uso:**
Una aplicación de videojuegos que almacena estadísticas de jugadores en tiempo real. DynamoDB gestiona millones de solicitudes sin necesidad de administrar servidores.

---

## 3. Creación y gestión de una base de datos en AWS

### 3.1 Creación de una instancia RDS

Para crear una instancia DS debes:

* Dirígirte a **Amazon RDS > Create database**.
* Seleccionar el motor (p. ej. PostgreSQL).

* Definir las credenciales de administrador.
* Eligir tipo de instancia (db.t3.micro, db.m5.large, etc.).

* Configurar almacenamiento, seguridad y red (VPC y subredes).
* Finalizar la creación y conectar tu aplicación o cliente SQL.

### 3.2 Gestión básica

- **Monitoreo:** Puedes utilizar *Amazon CloudWatch* para visualizar métricas (CPU, memoria, conexiones).
- **Copias de seguridad:** Puedes configurar backups automáticos diarios.
- **Escalado:** Puedes aumentar o reducir el tamaño de la instancia según la carga.

---

## 4. Controles de seguridad de la base de datos

La seguridad en bases de datos es esencial para proteger información sensible.
AWS incorpora medidas automáticas y configurables:

| Mecanismo                                        | Descripción                                                                                     |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| **Amazon IAM**                             | Controla qué usuarios o servicios pueden acceder a la base de datos.                            |
| **Security Groups**                        | Actúan como cortafuegos virtuales que filtran el tráfico entrante y saliente.                  |
| **Encriptación en reposo y en tránsito** | Usa claves gestionadas por AWS KMS para proteger los datos almacenados y las conexiones SSL/TLS. |
| **Auditoría y registros**                 | RDS y DynamoDB pueden registrar accesos y consultas para su análisis posterior.                 |

**Buenas prácticas :**

- Deshabilitar el acceso público cuando no sea necesario.
- Rotar contraseñas o claves de acceso periódicamente.
- Revisar los permisos de IAM para aplicar el principio de mínimo privilegio.

---

## 5. Migración de datos a bases de datos de AWS

Migrar datos a la nube es un proceso que puede implicar desde pequeños volúmenes de información hasta sistemas completos de producción.

### 5.1 Herramientas de migración

- **AWS Database Migration Service (DMS):**
  - Permite migrar datos desde bases de datos locales, otros servicios en la nube o entre motores diferentes.
  - Admite migraciones homogéneas (MySQL → MySQL) y heterogéneas (Oracle → Aurora).
  - Puede realizar la migración **sin detener la base de datos origen** (modo continuo).

### 5.2 Proceso típico

1. Configurar la base de datos origen y destino.
2. Crear una tarea de migración en AWS DMS.
3. Ejecutar pruebas para validar la integridad de los datos.
4. Cambiar la aplicación para conectarse a la nueva base.

### 5.3 Alternativas simples

- **Importación de archivos CSV o SQL** directamente en RDS o DynamoDB.
- **AWS DataSync** para mover grandes volúmenes de datos de forma automatizada.

---

## 6. Selección de tecnologías de almacenamiento

La elección del servicio adecuado depende de varios factores:

| Requisito                    | Servicio recomendado         | Motivo                                    |
| ---------------------------- | ---------------------------- | ----------------------------------------- |
| Aplicación web tradicional  | RDS (MySQL o Aurora)         | Relacional, consistente, soporta SQL      |
| Aplicación de IoT o juegos  | DynamoDB                     | Escalabilidad y baja latencia             |
| Alta disponibilidad crítica | Aurora Multi-AZ              | Réplicas automáticas, resiliencia       |
| Coste bajo y simplicidad     | RDS con instancias pequeñas | Configuración rápida y gestión mínima |

---

## 7. Conclusiones

AWS proporciona un ecosistema robusto para gestionar bases de datos de cualquier tipo y tamaño.
Ya sea mediante **RDS** para bases relacionales o **DynamoDB** para modelos NoSQL, los administradores pueden aprovechar la automatización, seguridad y escalabilidad de la nube.
