# Operación Rescate

## Incidencia 4 — El servidor privado no puede actualizar ni instalar paquetes

| Campo | Detalle |
| --- | --- |
| Ticket | INC-0004 |
| Prioridad | Alta |
| Reportado por | Equipo de Sistemas |
| Recurso afectado | Servidor privado |

**Descripción del usuario:** "El servidor `nova-update-ServerPrivado` (subred privada) necesita salir a Internet para ejecutar `dnf update` e instalar paquetes de seguridad. Cuando lo intentamos, el comando se queda colgado y termina con error de timeout. El servidor `nova-update-ServerPublico` sí tiene salida a Internet sin problemas. "

---

### Información adicional

- Las 2 instancias (cada una en una subred) aparecen en la consola como `running` y una de ellas dispone de IP pública.
- El servidor privado **no debe tener IP pública** ni ser accesible desde Internet. 
- Solo debe poder iniciar conexiones hacia fuera; nadie desde Internet debe poder iniciarlas hacia él.
- La solución debe aplicarse sin recrear la VPC ni las instancias.
- Esta VPC es independiente de las de los otros retos.

### Conexión por ssh a la instancia de la subred privada

- Las 2 instancias utilizan el par de claves `vockey` del laboratorio.
- Puedes copiar la clave desde tu máquina local a la mñáquina pública: `scp -i labsuser.pem labsuser.pem ec2-user@IP.PU.BLI.CA:/home/ec2-user`
- Puedes iniciar sesión por ssh en la máquina pública con la clave `labsuser.pem` y el comando `ssh -i labsuser.pem ec2-user@IP.PU.BLI.CA` y aprovechamos para cambiar los permisos del fichero recién copiado: `chmod 400 labsuser.pem`
- Como ya está copiada la clave, se puede acceder a la máquina privada por ssh: `ssh -i labsuser.pem ec2-user@IP.PRI.VA.DA`


### Tu misión

1. **Diagnostica** por qué el servidor privado no tiene salida a Internet. Documenta las comprobaciones que has hecho (tablas de rutas, asociaciones de subred, grupos de seguridad…).
2. **Diseña y aplica** una solución que cumpla las restricciones del ticket.
3. **Verifica** desde el servidor privado que la actualización funciona:
   ```bash
   sudo dnf update
   ```
4. **Comprueba** que se siguen cumpliendo las restricciones: el servidor privado sigue sin IP pública y no es alcanzable desde Internet.


!!! success "Captura las pantallas" 
    Captura las pantallas necesarias en las que se vean las modificaciones que has realizado y el acceso a internet desde la máquina de la subred privada (ejecuta `sudo dnf update`).
    
    Acompáñalas de una breve descripción de lo que has hecho para que funcione.

---
## Eliminación de los recursos

!!! danger "Atención $$$"
    Antes de eliminar la pila con CloudFormation debes eliminar manualmente el elemento que has necesitado crear en este reto para que funcionara. Es un elemento extremadamente caro que sigue consumiendo incluso con el laboratorio apagado.

!!! warning "Atención" 
    Una vez finalizados los retos, elimina la pila creada mediante CloudFormation para borrar todos los recursos. **Asegúrate que la pila está en estado DELETE_COMPLETE**


