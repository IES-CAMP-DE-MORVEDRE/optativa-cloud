# Operación Rescate

## Incidencia 3 — La aplicación no puede conectar con servicios externos seguros

| Campo | Detalle |
| --- | --- |
| Ticket | INC-0003 |
| Prioridad | Alta |
| Reportado por | Equipo de Desarrollo |
| Recurso afectado | Servidor de aplicación |

**Descripción del usuario:** "Nuestra aplicación necesita llamar a la API de un proveedor de pagos y a otros servicios que solo aceptan conexiones cifradas. Desde la migración, todas esas llamadas caducan por tiempo de espera. Con el equipo de redes hemos comprobado que la instancia sí puede salir hacia Internet en otras situaciones, así que no sabemos qué está pasando."

---

### Información adicional

- La instancia aparece en la consola como `running` y dispone de IP pública.
- La aplicación debe poder realizar conexiones HTTPS salientes a servicios externos.
- Esta VPC es independiente de las de los otros retos.
- Para comprobar si hay salida por el puerto HTTPS podemos ejecutar el comando `curl -I https://www.google.com`

### Tu misión
Permitir que la instancia establezca conexiones HTTPS salientes sin romper lo que ya funciona y sin ampliar permisos más de lo necesario.

!!! success "Captura las pantallas" 
    Captura las pantallas necesarias en las que se vean las modificaciones que has realizado y el acceso a internet por HTTPS desde la máquina que hace de servidor de aplicaciones mediante el comando `curl -I https://www.google.com`
    
    Acompáñalas de una breve descripción de lo que has hecho para que funcione.