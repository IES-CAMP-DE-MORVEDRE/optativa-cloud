# Práctica 5. CI/CD de una web estática en S3 mediante GitHub Actions

Implementación Continua/Despliegue Continuo de un sitio web estático en Amazon S3 mediante GitHub Actions.

CI/CD significa **Integración Continua (Continuous Integration)** y **Entrega/Despliegue Continuo (Continuous Delivery/Deployment)**.
Es un conjunto de prácticas que **automatizan la integración de código, las pruebas y el despliegue** de aplicaciones para entregar software de forma rápida y fiable.

**GitHub Actions** es una herramienta de **automatización integrada en GitHub** que permite ejecutar flujos de trabajo en respuesta a eventos del repositorio, como *push*, *pull request* o *merge*.

Se utiliza para implementar **CI/CD dentro de GitHub**, ya que permite **automatizar la integración, las pruebas y el despliegue del código** directamente desde el repositorio, sin necesidad de usar servicios externos.

En esta práctica utilizaremos GitHub Actions para automatizar la copia del repositorio a un Bucket S3 cada vez que se haga un commit en dicho repositorio. Esto implicará que cada vez que se haga un cambio de código, se suba automáticamente a AWS para estar disponible en la web.



## Objetivo de la práctica

* Comprender el funcionamiento del alojamiento web estático en Amazon S3.
* Aprender a crear un bucket, subir un sitio web y habilitar su acceso público **mediante una política de bucket**.
* Configurar S3 para que sirva páginas web (HTML, CSS, imágenes, etc.) directamente.
* Comprobar el acceso al sitio web a través de una URL pública de S3.


## Preparación del material

1.- En primer lugar vamos a hacer un fork a nuestra cuenta de GitHub del repositorio que utilizamos en la práctica 2 con una web de muestra. Lo haremos pulsanso sobre el botón `Fork` del repositorio.

- Valídate con tus credenciales en GitHub.
- Accede al repositorio de GitHub que contiene la web de muestra:
   [`https://github.com/ies-camp-de-morvedre/hello-cloud`](https://github.com/IES-CAMP-DE-MORVEDRE/hello-cloud).
- Pulsa en el botón **Fork**.
- Ya tienes en tu cuenta un repositorio con el mismo contenido.

---

## Creación del Bucket

## Creación del GitHub Action

Pulsar sobre `set up a workflow yourself`

Pegamos:
``` yaml
name: deploy static website to AWS-S3 - V2

on:
  push:
  
env:
  AWS_REGION: us-east-1
  
jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-session-token: ${{ secrets.AWS_SESSION_TOKEN }}
          aws-region: ${{env.AWS_REGION}}

      - name: Deploy to AWS S3
        run: aws s3 cp ./index.html s3://demo-unir-miss-2025

```

Hacemos commit y comprobamos que se nos ha creado un nuevo directorio en el repositorio con el fichero yaml que describe la acción a ralizar cuando hay un commit.
