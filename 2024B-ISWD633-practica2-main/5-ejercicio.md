## Esquema para el ejercicio
![Imagen](img/esquema-ejercicio5.PNG)

### Crear la red
docker network create net-wp

### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias
docker run -d --name mysql-container --network net-wp -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=wordpressdb -e MYSQL_USER=wordpressuser -e MYSQL_PASSWORD=wordpresspassword mysql:8


### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias
docker run -d --name wordpress-container --network net-wp -e WORDPRESS_DB_HOST=mysql-container:3306 -e WORDPRESS_DB_NAME=wordpressdb -e WORDPRESS_DB_USER=wordpressuser -e WORDPRESS_DB_PASSWORD=wordpresspassword -p 9300:80 wordpress

De acuerdo con el trabajo realizado, en la el esquema de ejercicio el puerto a es **9300**

Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.
![image](https://github.com/user-attachments/assets/465091bc-99c7-456c-9591-7f128b10ab3a)


Desde el panel de admin: cambiar el tema y crear una nueva publicación.
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
![image](https://github.com/user-attachments/assets/3eb41dab-addf-46e3-96b3-3c36f10ddde1)


### Eliminar el contenedor wordpress
docker rm -f wordpress-container

### Crear nuevamente el contenedor wordpress
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

### ¿Qué ha sucedido, qué puede observar?
Cuando se elimina y se vuelve a crear el contenedor de WordPress, si no se ha eliminado la base de datos MySQL, los datos de la base de datos (como publicaciones, configuraciones del sitio, etc.) seguirán estando presentes en ella. Sin embargo, si los datos no se han conservado correctamente o no se tienen un volumen configurado para la base de datos, se corre el riesgo de perder los datos almacenados en WordPress.






