### Crear contenedor de Postgres sin que exponga los puertos. Usar la imagen: postgres:11.21-alpine3.17
```
docker run -d --name postgres-container -e POSTGRES_PASSWORD=yourpassword postgres:11.21-alpine3.17
```

### Crear un cliente de postgres. Usar la imagen: dpage/pgadmin4
```
docker run -d --name pgadmin-container -e PGADMIN_DEFAULT_EMAIL=user@example.com -e PGADMIN_DEFAULT_PASSWORD=yourpassword -p 8080:80 dpage/pgadmin4
```

La figura presenta el esquema creado en donde los puertos son:
- a:  8080
- b:  80
- c:  5432

![Imagen](img/esquema-ejercicio3.PNG)

## Desde el cliente
### Acceder desde el cliente al servidor postgres creado.
![image](https://github.com/user-attachments/assets/15495436-c5a9-4997-817b-8d76221b20f2)
![image](https://github.com/user-attachments/assets/9e80c576-08a9-4d22-99bd-e6fae0ba2213)



### Crear la base de datos info, y dentro de esa base la tabla personas, con id (serial) y nombre (varchar), agregar un par de registros en la tabla, obligatorio incluir su nombre.

## Desde el servidor postgresl
### Acceder al servidor
### Conectarse a la base de datos info
```
\c info
```

### Realizar un select *from personas
![image](https://github.com/user-attachments/assets/e6cb0978-020b-4062-8746-f58cc8b47a67)

