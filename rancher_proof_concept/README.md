PRUEBA DE CONCEPTO DE RANCHEROS + RANCHER + KUBERNETES
======================================================

**Ingredientes:**

- docker toolbox instalado con docker-machine, alternativamente docker-machine en linux y virtualbox o KVM.

**Elaboración:**

1) Creacion de 3 maquinas virtuales. 1 maestro y 2 nodos de cluster.

docker-machine create -d virtualbox --virtualbox-boot2docker-url https://releases.rancher.com/os/latest/rancheros.iso rancher-master

docker-machine create -d virtualbox --virtualbox-boot2docker-url https://releases.rancher.com/os/latest/rancheros.iso rancher-node1

docker-machine create -d virtualbox --virtualbox-boot2docker-url https://releases.rancher.com/os/latest/rancheros.iso rancher-node2

2) Instalación de Rancher (Cluster Management Tool)

**cambiarnos al nodo maestro**

eval $(docker-machine env rancher-master)

**activar la version de cliente que corresponde con el servidor docker**

export DOCKER_API_VERSION=1.22

**testear que funciona la conexion**

docker ps

**instalar rancher tags -> latest o stable**

docker run -d --restart=always -p 8080:8080 rancher/server:latest

**visitar la pagina**

chrome `docker-machine ip rancher-master`:8080

3) Pasos necesarios para control de acceso

ADMIN -> Access Control.

pulsar local

Añadir cuenta de admin

Enable Local Auth

4) Configuración del entorno default para kubernetes

DEFAULT -> Manage Enviroments

pulsar 3 puntitos suspensivos verticales -> edit

pulsar kubernetes

Save

5) Añadir nodos al entorno

DEFAULT -> DEFAULT

Add Host

Save

copiar comando para añadir nodos:

debe de ser algo como:

sudo docker run -d --privileged -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/rancher:/var/lib/rancher rancher/agent:v1.0.1 http://192.168.99.101:8080/v1/scripts/<TOKEN>

6) ejecutar esa sentencia en ambos nodos

eval $(docker-machine env rancher-node1)

docker run -d --privileged -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/rancher:/var/lib/rancher rancher/agent:v1.0.1 http://192.168.99.101:8080/v1/scripts/<TOKEN>

eval $(docker-machine env rancher-node2)

docker run -d --privileged -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/rancher:/var/lib/rancher rancher/agent:v1.0.1 http://192.168.99.101:8080/v1/scripts/<TOKEN>

**a medida que se vayan uniendo iran apareciendo en la pagina web de rancher en INFRASTRUCTURE -> Hosts**

**se podrá comprobar que rancher empezará a desplegar ETCD y otros contenedores auxiliares para montar el cluster kubernetes**

7) Aplicacion hello-world-kubernetes (Guest Book)
TODO
