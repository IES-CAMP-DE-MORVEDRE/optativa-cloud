Perfecto 🔥 — te preparo una **práctica completa de laboratorio** de AWS centrada en **IAM, políticas y roles**, ideal para un entorno educativo (como el módulo de *Implantación de Sistemas Operativos* del ciclo de ASIR).

---

# 🧪 **Práctica: Creación y aplicación de políticas y roles en AWS**

### 🎯 **Objetivos**

* Comprender cómo funcionan las **políticas** y los **roles** en AWS IAM.
* Crear y aplicar una **política personalizada**.
* Asociar un **rol** a una **instancia EC2** para controlar el acceso a S3 sin usar credenciales.

---

## 🧭 **1️⃣. Preparación del entorno**

1. Accede a la **Consola de AWS**.
2. En el buscador superior, escribe **IAM** y entra al servicio.
3. Verifica que estás en la **región** donde crearás los recursos (por ejemplo, `eu-west-1`).

---

## 🧩 **2️⃣. Creación de una política personalizada**

### 🔸 Objetivo:

Permitir solo **lectura de objetos** dentro de un bucket S3 concreto.

### 🔸 Pasos:

1. En el panel lateral, selecciona **Policies → Create policy**.
2. Elige la pestaña **JSON** y pega lo siguiente:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::asir-lab-bucket",
        "arn:aws:s3:::asir-lab-bucket/*"
      ]
    }
  ]
}
```

3. Pulsa **Next**, asigna el nombre:
   👉 `LecturaS3Personalizada`
   y una descripción breve.
4. Crea la política.

📘 *Consejo:* sustituye `asir-lab-bucket` por el nombre real del bucket que usarás.

---

## 🧑‍💻 **3️⃣. Creación de un rol con permisos controlados**

### 🔸 Objetivo:

Permitir que una instancia **EC2** lea objetos del bucket S3 usando el rol (sin claves de acceso).

### 🔸 Pasos:

1. En **IAM → Roles → Create role**.
2. Selecciona **AWS service → EC2**, y haz clic en **Next**.
3. Adjunta la política recién creada **LecturaS3Personalizada**.
4. Asigna nombre al rol:
   👉 `rol-ec2-lectura-s3`.
5. Crea el rol.

---

## 💻 **4️⃣. Creación de la instancia EC2**

1. Ve al servicio **EC2 → Instances → Launch instance**.
2. Elige:

   * **AMI:** Amazon Linux 2 o Ubuntu.
   * **Tipo de instancia:** `t2.micro`.
3. En el apartado **IAM role**, selecciona **rol-ec2-lectura-s3**.
4. Lanza la instancia.

💡 *Este paso vincula la instancia con el rol IAM, otorgándole permisos temporales sin claves.*

---

## 🧰 **5️⃣. Verificación desde la instancia**

1. Conéctate a la instancia mediante **SSH**.

   ```bash
   ssh -i "clave.pem" ec2-user@<IP-PÚBLICA>
   ```
2. Instala la CLI de AWS (si no está instalada):

   ```bash
   sudo yum install -y awscli
   ```
3. Comprueba el acceso al bucket:

   ```bash
   aws s3 ls s3://asir-lab-bucket
   ```

📘 Si la política está bien configurada, verás el listado de objetos.
Si intentas subir un archivo, fallará:

```bash
aws s3 cp test.txt s3://asir-lab-bucket/
```

→ *AccessDenied* (porque la política solo permite lectura).

---

## 🔐 **6️⃣. Prueba con otro rol (ampliación opcional)**

1. Crea una nueva política llamada `EscrituraS3Personalizada`:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Action": ["s3:PutObject"],
         "Resource": ["arn:aws:s3:::asir-lab-bucket/*"]
       }
     ]
   }
   ```
2. Crea un nuevo rol **rol-ec2-escritura-s3** y asígnale esa política.
3. Cambia el rol de la instancia EC2:

   * EC2 → Instancia → pestaña **Security** → **Modify IAM role**.
   * Selecciona `rol-ec2-escritura-s3`.
4. Vuelve a probar el comando `aws s3 cp`.
   → Esta vez **debería funcionar**.

---

## 📋 **7️⃣. Limpieza del laboratorio**

Para evitar costes:

1. Detén o elimina la instancia EC2.
2. Elimina los roles creados.
3. Elimina las políticas personalizadas.
4. Si creaste buckets, bórralos si ya no los necesitas.

---

## 🧠 **Conclusiones**

* Las **políticas IAM** definen *qué acciones* se pueden realizar sobre *qué recursos*.
* Los **roles** permiten asignar permisos **a servicios o identidades temporales** sin usar credenciales.
* Las políticas pueden ser **muy específicas**, limitando el acceso a buckets, prefijos o acciones concretas.
* El modelo se basa siempre en el principio de **mínimos privilegios**.

---