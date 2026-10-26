---
layout: default
title: Inicio
nav_order: 1
description: "Introducción a la nube"
permalink: /
---


# Operación Rescate

## Contexto y escenario

Trabajas en el equipo de soporte cloud de **NovaLogística S.L.**, una pyme de transporte que ha movido cuatro de sus servicios a AWS. Esta mañana, el responsable de infraestructura ha dejado de estar disponible y ha dejado abiertas **cuatro incidencias** sin resolver. Cada una afecta a una instancia EC2 desplegada en una VPC distinta.

Tu misión es diagnosticar el origen de cada fallo y corregirlo con el menor cambio posible, dejando evidencia de todo el proceso.

## Entorno disponible
Para desplegar el laboratorio sigue los suguientes pasos:

- Descarga el fichero [operacion-rescate.yaml](./operacion-rescate.yaml)
- Inicia el laboratorio y en la consola de AWS accede al serivicio CloudFormation.
- Crea una nueva pila.
- Selecciona la opción *Cargar un archivo de plantilla* y sube el fichero `operacion-rescate.yaml` (o pega su contenido).
- Asigna un noimbre a la pila (por ejemplo *operacion-rescate*)
- Mantén `t3.micro` como tamaño de las instancias y `vockey`como par de claves.
- Espera a que el estado de la pila esté en `CREATE_COMPLETE`.
- En **Outputs**, tienes todas las IP públicas, los IDs de instancia, Security Groups y tablas de rutas creadas.
- Espera unos minutos a que termine `UserData` durante la creación de la instancia EC2 del reto 1. 

## Normas del laboratorio

- Cada incidencia es independiente: **no modifiques recursos de los otros retos**.
- Identifica la causa raíz **antes** de cambiar nada y guarda evidencia del estado inicial.
- Aplica la **corrección mínima**. No abras todos los puertos, no abras todo el tráfico y no sustituyas ni recrees recursos (instancias, VPC, subredes o gateways).
- No reutilices recursos de una VPC en otra.
- Los recursos pueden generar costes. Al terminar la práctica, elimina la pila.

!!! warning "Atención" 
    Una vez finalizados los retos, elimina la pila creada mediante CloudFormation para borrar todos los recursos.

## Conexión a las máquinas

- Podemos abrir sesión en cada una de las instancias desde la propia consola gráfica del navegador mediante la opción de **Conectar** dentro del apartado de instancias EC2.
- Para conectarnos a una instancia alojada en una **subred pública** utilizaremos la opción **Conexión de la instancia EC2**.
- Para la conexión a una instancia dentro de una **subred privada** no tenemos más remedio que conectarnos a la instancia de la subred pública y desde ahí (mediante la clave previamente copiada) conectarnos a la privada.

## Pistas

- Puertos y protocolos:

    - SSH: TCP/22, administración remota.
    - HTTP: TCP/80, acceso web sin cifrar.
    - HTTPS: TCP/443, conexiones web cifradas.

- `0.0.0.0/0` es una notación CIDR que representa todas las direcciones IPv4 posibles. Suele utilizarse para hacer referencia al tráfico dirigido/procedente de cualquier dirección IPv4.

