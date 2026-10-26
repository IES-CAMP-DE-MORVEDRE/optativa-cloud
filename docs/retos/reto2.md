# Operación Rescate

## Incidencia 2 — El servidor de informes no tiene salida a Internet

| Campo | Detalle |
| --- | --- |
| Ticket | INC-0002 |
| Prioridad | Media |
| Reportado por | Equipo de Análisis de Datos |
| Recurso afectado | Servidor de informes |

**Descripción del usuario:** "El servidor de informes tiene que descargar actualizaciones y datos externos cada noche, pero no consigue conectarse a ningún sitio de Internet. Nos han confirmado que la máquina tiene una IP pública asignada, así que no entendemos por qué no sale."

---

### Información adicional

- La instancia aparece en la consola como `running` y dispone de IP pública.
- Esta VPC es independiente de las de los otros retos y tiene sus propios recursos de red.
- Lo que falla es el tráfico hacia Internet, no el funcionamiento interno de la instancia.

### Tu misión

Hacer que la subred de la instancia pueda encaminar tráfico hacia Internet y demostrar, con la configuración corregida, que la salida queda habilitada.

!!! success "Captura las pantallas" 
    Captura las pantallas necesarias en las que se vean las modificaciones que has realizado y el acceso a internet desde la máquina que hace de servidor de informes.
    
    Acompáñalas de una breve descripción de lo que has hecho para que funcione.