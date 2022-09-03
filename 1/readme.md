# Ejercicios

**Namespace a usar: `educacionit`**

## Ejercicio 1
```
Despliega en Kubernetes una aplicación web “webapp”
Imagen:  roxsross12/web:v1
Puerto: 5000
Crea un servicio para ella
Accede a ella desde el navegador web
```

## Ejercicio 2
```
Escala el deployment de webapp para que tenga dos réplicas
Comprueba que si se crean esas réplicas
Verifica que al acceder a la web cada vez se obtiene una IP diferente porque se accede a un contenedor diferente
````

## Ejercicio 3
Despliega una aplicación de web de anuncios con base de datos en Kubernetes

### Aplicación Web
```
Imagen: roxsross12/java-webapp-bbdd:v2
Puerto: 8080
Variables de entorno: 
MYSQL_ROOT_PASSWORD = pass
MYSQL_DATABASE = test
Base de datos:

Imagen: mysql:5.6
Puerto: 3306
Nombre del servicio: db
Variables de entorno
MYSQL_ROOT_PASSWORD=pass
MYSQL_DATABASE=test
```