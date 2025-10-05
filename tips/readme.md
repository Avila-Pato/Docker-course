# Montando un contenedor

1. Montar la imagen de MariaDB con el tag jammy, publicar en el puerto 3306 del contenedor con el puerto 3306 de nuestro equipo, colocarle el nombre al contenedor de world-db (--name world-db) y definir las siguientes variables de entorno:

- MARIADB_USER=example-user
- MARIADB_PASSWORD=user-password
- MARIADB_ROOT_PASSWORD=root-secret-password
- MARIADB_DATABASE=world-db
- Conectarse usando Table Plus a la base de datos con las credenciales del usuario (NO EL ROOT)

2. Conectarse a la base de datos world-db

3. Ejecutar el query de creación de tablas e inserción proporcionado

4. Revisar que efectivamente tengamos la data


> [!IMPORTANT]  
> Para borrar un contenedor: docker container rm -f <nombre_o_id> <--- las tres ultimos caracteres


```
docker container run `
 -d -p 3306:3306 `
 --name world-db `
 --env MARIADB_USER=example-user `
 --env MARIADB_PASSWORD=root-secret-password `
 --env MARIADB_ROOT_PASSWORD=root-secret-password `
 --env MARIADB_DATABASE=world-db `
 mariadb:jammy
```

# Volumenes y persistencia

```
docker container run `
 -d -p 3306:3306 `
 --name world-db `
 --env MARIADB_USER=example-user `
 --env MARIADB_PASSWORD=root-secret-password `
 --env MARIADB_ROOT_PASSWORD=root-secret-password `
 --env MARIADB_DATABASE=world-db `
 --volume world-db:/var/lib/mysql `
 mariadb:jammy
```
-  en el comando --volume world-db:/var/lib/mysql, world-db es el nombre que le da al volumen que se va a crear en nuestra máquina y el /var/lib/mysql es la ruta donde el contenedor guarda los datos, esta ruta normalmente la proporciona la documentación de la imagen en Docker Hub.



# levantando un contenedor php

- version: phpmyadmin:5.2.0-apache

```
docker run -d \
  --name my-phpmyadmin \
  -e PMA_HOST=localhost \
  -p 8080:80 \
  phpmyadmin:5.2.0-apache
```

- -d → corre el contenedor en segundo plano.

- --name my-phpmyadmin → le da un nombre al contenedor.

- -e PMA_HOST=localhost → le indica a phpMyAdmin el host del servidor MySQL/MariaDB al que conectarse (si tu contenedor de MariaDB se llama world-db, pon PMA_HOST=world-db).

- -p 8080:80 → expone el puerto 80 del contenedor en el puerto 8080 de tu máquina.
