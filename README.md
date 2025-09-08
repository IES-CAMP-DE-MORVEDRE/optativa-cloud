# OPTATIVA-AWS
Asignatura optativa AWS

## Para montar un entorno de prueba local
Estando situado en el directorio del proyecto, ejecutar:

```
docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material
```

y luego abrir en el navegador http://localhost:8000
