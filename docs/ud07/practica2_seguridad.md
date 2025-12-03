# Práctica 2 – Seguridad en Red, Roles IAM y Auditoría

## Objetivo

Crear una arquitectura segura con VPC, EC2, roles IAM y auditoría con CloudTrail.

## Escenario

La empresa "NetSecure" necesita:

- Una EC2 accesible solo por SSH desde la IP del estudiante.
- EC2 debe leer un bucket S3 usando IAM Roles.
- Registrar todas las acciones con CloudTrail.

<img src="../images/ud07/practica/ud07_p02.png" width=600>

## Tareas

### 1. Crear VPC

- Nombre: `netsecure-vpc`
- CIDR: `10.0.0.0/16`

### 2. Crear subnet pública

- Nombre: `public-subnet-1`
- CIDR: `10.0.1.0/24`

### 3. Crear Internet Gateway

- Asociarlo a `netsecure-vpc`.

### 4. Crear Route Table pública

- Asociar a `public-subnet-1`.
- Añadir ruta a `0.0.0.0/0` → IGW.

### 5. Crear Security Group

- Nombre: `sg-ec2-netsecure`.
- Inbound: SSH desde “My IP”.
- Outbound: permitir todo.

### 6. Crear bucket S3

- Nombre: `netsecure-app-storage`.

### 7. Crear rol IAM para EC2

- Trusted entity: EC2.
- Política: `AmazonS3ReadOnlyAccess`.
- Nombre: `EC2-S3-Role`.

### 8. Lanzar EC2

- Amazon Linux 2.
- Subnet: `public-subnet-1`.
- SG: `sg-ec2-netsecure`.
- Rol IAM: `EC2-S3-Role`.

### 9. Acceder por SSH

```bash
ssh -i clave.pem ec2-user@IP_PUBLICA
```

### 10. Verificar acceso a S3 sin claves

En la EC2:

```bash
aws s3 ls s3://netsecure-app-storage
```

### 11. Activar CloudTrail

- Crear trail `netsecure-trail`.
- Grabar logs en un nuevo bucket.



!!! success "Captura las pantallas"   
    Acceso por ssh a la EC2  
    Acceso a S3 sin claves  
    Resultado de realizar acciones en IAM/EC2" y observar eventos en CloudTrail → Event History  

