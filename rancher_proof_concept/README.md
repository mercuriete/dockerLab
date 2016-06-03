PRUEBA DE CONCEPTO DE RANCHEROS + RANCHER + KUBERNETES
======================================================

Ingredientes:
- docker toolbox instalado con docker-machine, alternativamente docker-machine en linux y virtualbox o KVM.

Elaboración:

1) Creacion de 3 maquinas virtuales. 1 maestro y 2 nodos de cluster.

docker-machine create -d virtualbox --virtualbox-boot2docker-url https://releases.rancher.com/os/latest/rancheros.iso rancher-master
docker-machine create -d virtualbox --virtualbox-boot2docker-url https://releases.rancher.com/os/latest/rancheros.iso rancher-node1
docker-machine create -d virtualbox --virtualbox-boot2docker-url https://releases.rancher.com/os/latest/rancheros.iso rancher-node2

2) TODO
