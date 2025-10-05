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

> [!TIPS]
> Mostrar contenedor: docker container ls
> Mostrar imagenes:  docker image ls  


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
docker container run  \
  --name my-phpmyadmin \
  -d \
  -e PMA_ARBITRARY=1 \
  -p 8080:80 \
  phpmyadmin:5.2.0-apache
```

- -d → corre el contenedor en segundo plano.

- --name my-phpmyadmin → le da un nombre al contenedor.

- -e PMA_HOST=localhost → permite conectarte a cualquier servidor MySQL/MariaDB, incluso si no está en la misma red de Docker

- -p 8080:80 → expone el puerto 80 del contenedor en el puerto 8080 de tu máquina.

- Accedes desde http://localhost:8080 y podras ver el host, usuario y contra, para esta oportunidad  example-user  es neustro usuario y  secret-password es nuestra password

> [!IMPORTANT]  
> Redes!
> Regla de oro
> si dos o mas contenedores estan en la misma red, podran hablar entre si. Si no lo estan no podran.
> por ende habra que hacer referencia entre phpmyadmin y world-db que es nuestro servidor

# Redes y contenedores

> [!TIP]
> docker network: lista de comandos para network 





