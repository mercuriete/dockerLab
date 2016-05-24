<<  [Principal](http://erasmolpa.github.io/dockerLab)

#  Docker Compose

##  Contenido:

	* Docker [Compose](#compose). Orquestando Servicios.
      
      
see   https://docs.docker.com/compose/env-file/
      https://docs.docker.com/compose/reference/
      https://docs.docker.com/compose/compose-file/

### Compose. Primeros pasos:

Docker [Compose](https://docs.docker.com/compose/) es una herramienta para definir y correr aplicaciones multicontenedores. Mediante un fichero de configuración, docker-compose.yml, orquestamos y "linkamos" nuestros contenedores.
Es una muy buena opción para proyectos con arquitecturas mutliservicios, aplicaciones monolíticas (Servidor aplicacion + servidor web + base de datos) y muy útil para definir ciclos de integración contínua.

#### Instalación. Sólo Para Linux.
```
$ curl -L https://github.com/docker/compose/releases/download/1.6.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```
```
$ chmod +x /usr/local/bin/docker-compose

```
##### Comprobamos la instalación
```
$ docker-compose --version
```
##### **En máquinas Mac y Windows ya viene instalado como parte de Docker Toolbox.**

#### Comandos Docker Compose.
```
$ docker-compose up
```
##### Si se quiere pasar como argumento el fichero de especificación:

```
$ docker-compose -f  fichero.yml up
```
##### Ejecutar en segundo plano:
```
$ docker-compose -f <fichero> up -d
```
#####Parar un entorno:
```
$ docker-compose -f <fichero> kill
```
#####Para ver los contenedores parados se haría
```
$ docker ps -a
```
#####Eliminar por completo un entorno:
```
$ docker-compose -f <fichero.yml> rm
```
#####Comprobar los logs de los contenedores (lo explicado en el primer punto):
```
$ docker-compose logs
```
#####Comprobar un fichero con la especificación yml del entorno
```
$ docker-compose -f <fichero.yml> config
```

Existe un [repositorio](https://stackfiles.io/) de Stacks files que se pueden reutilizar. Además en Dicker Hub tienes múltiples de instalaciones compose que pueden servir de guía como la que veremos a continuación


#### Usando Compose:

Creando un contenedor wordpress y mariaDb

Si accedemos al hub de  oficial de [wordpress](https://hub.docker.com/_/wordpress/) vemos que proponen dos medios de crear una web.Tanto utilizando links containers como usando compose. El fichero compose es el siguiente :

Ejemplo **docker-compose.yml** para wordpress:
 `
 <pre>
 wordpress:
  image: wordpress
  links:
    - db:mariadb
  ports:
    - 8080:80
db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: example
 <code>
 
 Finalmente lanzamos compose donde tengamos el fichero docker-compose.yml
 ```
  $ docker-compose up 
```
En la url http://192.168.99.100:8080/wp-admin/install.php , es decir en la http://host-ip:8080.


En la sección de [Ejercicios Compose](https://github.com/erasmolpa/dockerLab/blob/master/Ejercicios.md) haremos varios ejemplos de compose.
