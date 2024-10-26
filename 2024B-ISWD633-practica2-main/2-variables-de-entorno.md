# Variables de Entorno
### ¿Qué son las variables de entorno?
```
Las variables de entorno son pares clave-valor que se utilizan para configurar el comportamiento de los procesos del sistema o de las aplicaciones que se están ejecutando. Estas variables permiten que las aplicaciones o scripts reciban información sobre el entorno en el que están trabajando, como las rutas de los directorios, las credenciales de acceso, los modos de configuración (desarrollo, producción, etc.), y otros valores necesarios.
```

### Para crear un contenedor con variables de entorno?

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.
```
docker run -d --name nginx-container -e username=user123 -e role=admin nginx:alpine
```

# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR

![image](https://github.com/user-attachments/assets/40596973-529c-4658-ba47-d5531b6993e4)

### Crear un contenedor con mysql:8 , mapear todos los puertos

```
docker run -d --name mysql-container -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=mydb -P mysql:8
```

### ¿El contenedor se está ejecutando?

```
PS C:\Users\User> docker psCONTAINER ID   IMAGE                              COMMAND                  CREATED          STATUS          PORTS                                               NAMESc3df390e1080   mysql:8                            "docker-entrypoint.s…"   5 minutes ago    Up 5 minutes    0.0.0.0:32768->3306/tcp, 0.0.0.0:32769->33060/tcp   mysql-containerae959862a4f6   nginx:alpine                       "/docker-entrypoint.…"   12 minutes ago   Up 12 minutes   80/tcp                                              nginx-container14d001f51c1c   jenkins/jenkins:alpine3.18-jdk11   "/sbin/tini -- /usr/…"   3 hours ago      Up 3 hours      0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp    jenkins-container

```
### Identificar el problema
```
docker logs mysql-container
```

### Eliminar el contenedor creado con mysql:8 
```
docker rm mysql-container
```

### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

Previo a esto es necesario crear el archivo y colocar las variables en un archivo, **.env** se ha convertido en una convención estándar, pero también es posible usar cualquier extensión como **.txt**.
```
docker run -d --name <nombre contenedor> --env-file=<nombreArchivo>.<extensión> <nombre imagen>
```
**Considerar**
Es necesario especificar la ruta absoluta del archivo si este se encuentra en una ubicación diferente a la que estás ejecutando el comando docker run.

### Crear un contenedor con mysql:8 , mapear todos los puertos y configurar las variables de entorno mediante un archivo
```
docker run -d --name mysql-container --env-file="C:\Users\User\Downloads\mysql.env" -P mysql:8 
```
# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR 
![image](https://github.com/user-attachments/assets/df165fc7-b47e-4adc-b0de-5323f86a46a1)


### ¿Qué bases de datos existen en el contenedor creado?
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| mydb               |
+--------------------+
