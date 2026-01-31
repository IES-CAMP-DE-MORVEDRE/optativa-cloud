# Proyecto DAW_T 2ª Evaluación:

## 1. Objetivo del proyecto

El objetivo de este proyecto es diseñar y desplegar en **AWS** una arquitectura cloud completa que permita:

1. Obtener datos desde una API pública externa.  
2. Almacenar dichos datos en una base de datos situada en una subred privada.  
3. Mostrar los datos almacenados mediante una aplicación web accesible desde Internet.

El proyecto simula un caso real de uso profesional, integrando redes, cómputo, almacenamiento, microservicios y seguridad básica en la nube pública.

---

## 2. Arquitectura mínima obligatoria

### 2.1 Infraestructura de red

El alumnado deberá desplegar, como mínimo:

- Una **VPC** propia del proyecto.
- Una **subred pública**, que contendrá:
  - La aplicación web frontend.
  - Acceso a Internet mediante **Internet Gateway (IGW)**.
- Una **subred privada**, que contendrá:
  - El microservicio de ingesta de datos.
  - La base de datos.
- Tablas de rutas correctamente configuradas.
- Grupos de seguridad diferenciados para:
  - Frontend web.
  - Backend / microservicio.
  - Base de datos.

⚠️ La base de datos **no debe ser accesible directamente desde Internet**.

---

## 3. Base de datos

- La base de datos debe estar obligatoriamente en una subred privada.
- Puede utilizarse:
  - **RDS** (MySQL o PostgreSQL), o
  - Una instancia **EC2** con motor de base de datos instalado.
- El acceso debe estar restringido únicamente al backend.
- Se debe realizar al menos un **backup o snapshot** antes de la entrega.

---

## 4. Microservicio de ingesta

El proyecto debe incluir un microservicio que:

- Consuma datos desde una API pública externa autorizada.
- Procese los datos recibidos (JSON / CSV).
- Inserte los datos en la base de datos.
- Se ejecute de forma periódica (cron, tarea programada o similar).

**Requisitos obligatorios:**

- La API key debe almacenarse en **variables de entorno**.
- El microservicio debe ejecutarse en la **subred privada**.

---

## 5. Aplicación web pública

- Debe estar desplegada en la subred pública.
- Debe mostrar datos reales almacenados en la base de datos.
- Acceso mediante navegador (IP pública o DNS).
- Puede implementarse con **Apache** o como **S3**.

Debe demostrarse claramente la **lectura desde la base de datos**.

---

## 6. Seguridad y observabilidad

El proyecto debe aplicar, al menos:

- Grupos de seguridad sin puertos innecesarios abiertos.
- Gestión correcta de claves y credenciales.
- Logs básicos de la aplicación.
- Al menos una métrica o alarma en **CloudWatch**.

---

## 7. Entregables obligatorios

El alumnado deberá entregar:

1. **Diagrama de arquitectura**.
2. **Código fuente** (ZIP o repositorio privado):
   - Microservicio.
   - Aplicación web.
   - `README` con instrucciones de despliegue y uso.
3. **Capturas de pantalla**, cada una con explicación técnica breve (2–3 líneas):
   - VPC y subredes.
   - Tablas de rutas.
   - Grupos de seguridad.
   - Instancias / servicios desplegados.
   - Base de datos.
   - Backup o snapshot.
   - CloudWatch.
   - Web funcionando.
4. **Documento técnico** (máx. 2 páginas):
   - Medidas de seguridad.
   - Estimación básica de costes.
5. **URL o IP pública funcional**.

---

## 8. Normas generales

- APIs gratuitas, sin tarjeta de crédito (registro simple permitido).
- Frecuencia de consulta limitada.
- Cada grupo/alumno utilizará una API distinta y/o endpoints claramente diferenciados.
- Copias o reutilización de proyectos: **calificación 0**.

---

## 9. Lista oficial de APIs autorizadas

### Meteorología
1. OpenWeatherMap  
   https://openweathermap.org/api  
2. WeatherAPI  
   https://www.weatherapi.com/docs/  
3. WeatherStack  
   https://weatherstack.com/documentation  
4. AEMET OpenData  
   https://opendata.aemet.es/

### Bolsa y divisas
5. Alpha Vantage  
   https://www.alphavantage.co/documentation/  
6. ExchangeRate API  
   https://www.exchangerate-api.com/docs/overview  
7. Finnhub  
   https://finnhub.io/docs/api

### Deportes
8. TheSportsDB  
   https://www.thesportsdb.com/api.php  
9. API-Football (RapidAPI)  
   https://rapidapi.com/api-sports/api/api-football/

### Ciencia y datos generales
10. NASA Open APIs  
    https://api.nasa.gov/  
11. OpenAQ  
    https://docs.openaq.org/

### Datos públicos y open data
12. MITECO – Embalses (datos.gob.es)  
    https://datos.gob.es/  
13. EMT Madrid / EMT València  
    https://opendata.emtmadrid.es/  
    https://www.emtvalencia.es/geo/

### Datos estructurados
14. PokéAPI  
    https://pokeapi.co/docs/v2  
15. Nominatim (OpenStreetMap)  
    https://nominatim.org/release-docs/latest/api/Overview/

---

## 10. Criterios generales de evaluación

- Infraestructura y redes: **25 %**
- Microservicio y despliegue: **25 %**
- Base de datos y almacenamiento: **20 %**
- Seguridad: **15 %**
- Documentación, pruebas y demostración: **15 %**
