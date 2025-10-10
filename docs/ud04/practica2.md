# Práctica 2. Publicación de una web estática en S3

Publicación de un sitio web estático en Amazon S3 con control de acceso mediante políticas de bucket.

<img src="../images/ud04/practica1/bucket00.png" width="600">

## Objetivo de la práctica

* Comprender el funcionamiento del **alojamiento web estático** en Amazon S3.
* Aprender a **crear un bucket**, **subir un sitio web** y **habilitar su acceso público mediante una política de bucket**.
* Configurar S3 para que sirva **páginas web (HTML, CSS, imágenes, etc.)** directamente.
* Comprobar el acceso al sitio web a través de una **URL pública de S3**.


## 🪣 **Parte 1. Preparación del material**

1. Accede al **repositorio de GitHub** de la práctica (por ejemplo:
   `https://github.com/usuario/nombre-repo`).
2. Descarga el repositorio en formato **ZIP** pulsando en **Code → Download ZIP**.
3. Descomprime el archivo ZIP en tu equipo local. Deberías tener una carpeta con archivos como `index.html`, `style.css`, `imagenes/`, etc.

---

## 🧱 **Parte 2. Creación del bucket**

1. Inicia sesión en la **Consola de AWS** y entra en el servicio **S3**.
2. Haz clic en **“Crear bucket”**.
3. Completa los campos:

   * **Nombre del bucket:** por ejemplo, `asir-web-estatica-nombrealumno`.
   * **Región:** elige una cercana, como **Europa (Irlanda)**.
4. En la sección **“Bloquear el acceso público”**, **desmarca** la casilla *“Bloquear todo el acceso público”*.

   > ⚠️ Esto se hace solo con fines educativos. En entornos reales se usarían mecanismos más seguros.
5. Pulsa **“Crear bucket”**.

---

## 📤 **Parte 3. Subir los archivos de la web**

1. Entra en el bucket creado.
2. Haz clic en **“Cargar” → “Añadir archivos”** y selecciona todos los archivos y carpetas del sitio web.
3. Pulsa **“Cargar”** y espera a que finalice el proceso.

---

## ⚙️ **Parte 4. Activar el alojamiento web estático**

1. En la vista del bucket, abre la pestaña **“Propiedades”**.
2. Busca la sección **“Alojamiento de sitio web estático”**.
3. Haz clic en **“Editar”** → selecciona **“Habilitar”**.
4. En **Documento de índice**, escribe:

   ```
   index.html
   ```
5. (Opcional) Si tu web tiene página de error, indícalo en **Documento de error**, por ejemplo:

   ```
   error.html
   ```
6. Pulsa **“Guardar cambios”**.
7. Copia la **URL del sitio web** que aparece (por ejemplo:
   `http://asir-web-estatica-nombrealumno.s3-website-eu-west-1.amazonaws.com`).

---

## 🔒 **Parte 5. Configurar la política del bucket**

1. Ve a la pestaña **“Permisos”** del bucket.

2. Localiza **“Política de bucket”** y pulsa **“Editar”**.

3. Pega la siguiente **política JSON**, sustituyendo el nombre del bucket por el tuyo:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "PublicReadGetObject",
         "Effect": "Allow",
         "Principal": "*",
         "Action": "s3:GetObject",
         "Resource": "arn:aws:s3:::asir-web-estatica-nombrealumno/*"
       }
     ]
   }
   ```

4. Guarda los cambios.

   > Esta política permite que **cualquiera pueda leer los archivos del bucket**, pero **no modificarlos ni borrarlos**.

---

## 🌍 **Parte 6. Comprobar el funcionamiento**

1. Abre la **URL del sitio web** copiada en la parte 4.
2. Si todo está correcto, tu página `index.html` se mostrará públicamente.
3. Prueba a acceder a imágenes o archivos directamente desde el navegador usando su ruta, por ejemplo:

   ```
   http://asir-web-estatica-nombrealumno.s3-website-eu-west-1.amazonaws.com/imagenes/logo.png
   ```
4. Si aparece un error 403 (Forbidden), revisa que:

   * Has desactivado el bloqueo de acceso público.
   * La política de bucket se guardó correctamente.
   * Los nombres de archivo coinciden (mayúsculas/minúsculas incluidas).

---

## ✅ **Comprobaciones finales**

* ¿La web se carga correctamente desde la URL de S3?
* ¿El acceso se ha controlado mediante **política de bucket**, no ACL?
* ¿El documento de índice se muestra automáticamente?
* ¿Has entendido la diferencia entre **alojamiento web estático** y **almacenamiento de objetos privado**?




Práctica 1 --> Crear bucket, subir contenido y acceder a él (Con ACLs). Control de versiones.

Práctica 2 --> Crear web estática en bucket S3 (Con políticas)

Práctica 3 --> Práctica guiada EBS. Creación de un volumen e instantánea y montaje en otra instancia. Última parte creación de un volumen en otra instancia, formateo y montaje manual.

Práctica 4 --> Práctica guiada EFS.

Práctica 5 (Opcional) --> CI/CD Web estática en S3 desde Github

https://aitor-medrano.github.io/bigdata2122/apuntes/nube04almacenamiento.html

https://aitor-medrano.github.io/iabd/cloud/s3.html
