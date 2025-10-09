# Práctica 1. Creación de un bucket en Amazon S3

Creación y gestión de un bucket en Amazon S3: subida de objetos, control de permisos y versiones.

## Objetivo de la práctica

* Comprender el funcionamiento de Amazon S3 como servicio de almacenamiento de objetos.
* Aprender a crear y configurar un bucket en una región determinada.
* Subir archivos y gestionar su acceso mediante ACLs.
* Acceder a un objeto público a través de su URL en el navegador.
* Activar el control de versiones y comprobar cómo mantiene distintas versiones de un mismo archivo.

## Práctica a realizar

### Parte 1. Creación del bucket

1. Inicia sesión en la **Consola de AWS** y entra en el servicio **S3**.
2. Pulsa en **“Crear bucket”**.
3. Especifica:

   * **Nombre del bucket:** debe ser único (por ejemplo: `asir-practica-s3-nombrealumno`).
   * **Región:** elige una cercana, por ejemplo **Europa (Irlanda)**.
4. En “**Configuración de permisos**”, **desactiva el bloqueo del acceso público** (solo para esta práctica).
5. Crea el bucket pulsando **“Crear bucket”**.



### Parte 2. Subida de objetos

1. Entra en el bucket recién creado.
2. Pulsa **“Cargar”** → **“Añadir archivos”** y selecciona 2 o 3 imágenes.
3. Haz clic en **“Cargar”** para subirlas.
4. Comprueba que aparecen en la lista de objetos.

---

### Parte 3. Cambiar permisos mediante ACL

1. Selecciona una de las imágenes subidas.
2. En la pestaña **“Permisos”**, busca la sección **“Listas de control de acceso (ACL)”**.
3. Pulsa en **“Editar”** y concede permiso de **lectura pública** al objeto (lectura para “Todos los usuarios”).
4. Guarda los cambios.

!!! danger "Atención"
    En entornos reales **no se deben dejar objetos públicos**.

---

### Parte 4. Acceso mediante URL

1. Vuelve a la pestaña **“Propiedades”** del objeto.
2. Copia la **URL del objeto** (por ejemplo:
   `https://asir-practica-s3-nombrealumno.s3.eu-west-1.amazonaws.com/foto1.jpg`)
3. Abre un **navegador web** y pega la URL.
4. Comprueba que la imagen se muestra correctamente (gracias al permiso público).

---

### Parte 5. Activar el control de versiones

1. Regresa a la vista principal del bucket.
2. En la pestaña **“Propiedades”**, busca la sección **“Control de versiones”**.
3. Pulsa **“Editar”** → activa el **control de versiones** → **Guardar cambios**.

---

### Parte 6. Probar el control de versiones

1. Sube **de nuevo una imagen con el mismo nombre** que una ya existente (por ejemplo `foto1.jpg`).
2. S3 **no reemplazará** la imagen anterior, sino que guardará **una nueva versión**.
3. Ve al objeto y selecciona la pestaña **“Versiones”** para ver las distintas versiones almacenadas.
4. Prueba a **descargar o restaurar** la versión anterior.

---

###  Comprobaciones finales

* ¿Puedes acceder a la imagen pública desde el navegador?
* ¿El bucket tiene el control de versiones activado?
* ¿Aparecen varias versiones del mismo archivo?



Práctica 1 --> Crear bucket, subir contenido y acceder a él (Con ACLs). Control de versiones.

Práctica 2 --> Crear web estática en bucket S3 (Con políticas)

Práctica 3 --> Práctica guiada EBS. Creación de un volumen e instantánea y montaje en otra instancia. Última parte creación de un volumen en otra instancia, formateo y montaje manual.

Práctica 4 --> Práctica guiada EFS.

Práctica 5 (Opcional) --> CI/CD Web estática en S3 desde Github

https://aitor-medrano.github.io/bigdata2122/apuntes/nube04almacenamiento.html

https://aitor-medrano.github.io/iabd/cloud/s3.html
