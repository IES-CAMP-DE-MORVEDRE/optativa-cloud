# Práctica 1 – Control de Acceso con IAM y Políticas

## Objetivo

Comprender usuarios, grupos, roles, políticas y el principio de mínimos privilegios mediante un escenario realista.

## Escenario

La empresa "TechEdu" quiere gestionar el acceso a materiales en un bucket S3:

- Profesores: lectura, subida y borrado.
- Alumnos: solo lectura.
- Invitados: sin acceso.

<img src="../images/ud07/practica/ud07_p01.png" width=600>

## Tareas

### 1. Crear bucket S3

- Nombre: `techedu-material`.
- Bloquear acceso público.

### 2. Crear grupos IAM

- `Profesores`
- `Alumnos`

### 3. Crear usuarios

- `profesor1` → Profesores
- `alumno1` → Alumnos
- `invitado1` → sin grupo

### 4. Crear políticas personalizadas

#### Profesores (acceso completo al bucket):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:*"],
      "Resource": [
        "arn:aws:s3:::techedu-material",
        "arn:aws:s3:::techedu-material/*"
      ]
    }
  ]
}
```

#### Alumnos (solo lectura):

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
        "arn:aws:s3:::techedu-material",
        "arn:aws:s3:::techedu-material/*"
      ]
    }
  ]
}
```

!!! success "Captura las pantallas"  
    Captura la pantalla donde se vea que `alumno1` puede leer pero no subir ni borrar.  
    Captura la pantalla donde se vea que`profesor1` puede leer, subir y borrar.  
    Captura la pantalla donde se vea que `invitado1` recibe *Access Denied* en todo.  
