---
title: Instalar Wireguard VPN en Docker
published: true
---
En esta practica voy a explicar el proceso para configurar Wireguard VPN dentro de Docker.

### Instalación de Wireguard

Lo primero como siempre en ubuntu es actualizar los repositorios y el sistema.

```bash
sudo apt update
sudo apt upgrade
sudo apt install docker docker-compose
```
![](/assets/Practica13 VPN/parte2/1.png)
![](/assets/Practica13 VPN/parte2/2.png)

### Creación del contenedor

Para crear el contenedor usaremos el siguiente comando. Esto creará un contenedor con el nombre wireguard,con la hora de Madrid, escuchando en el puerto 51820, y utilizando la imagen de Wireguard. Además guarda la configuración en caso de que se reinicie el servidor.
```bash
docker run -d --name wireguard --cap-add=NET_ADMIN --cap-add=SYS_MODULE -e PUID=1000 -e PGID=1000 -e TZ=Europe/Madrid -e SERVERURL=auto -e PEERS=laptop,tablet,phone -e PEERDNS=auto -p 51820:51820/udp -v wireguard_config:/config -v /lib/modules:/lib/modules --sysctl="net.ipv4.conf.all.src_valid_mark=1" --restart=unless-stopped linuxserver/wireguard
```

![](/assets/Practica13 VPN/parte2/3.png)

Dado que hemos especificado que queremos de peers laptop,tablet y phone, al arrancar el contenedor se generarán los QRs necesarios para que estos se conecten al servidor sin necesidad de mayor configuración. Pero en este caso vamos a conectarnos mediante el cliente de Wireguard para Windows. Así que podemos omitir esa orden a la hora de crear el contenedor.

![](/assets/Practica13 VPN/parte2/4.png)




### Configuración del contenedor

Ahora que ya está corriendo el contenedor, vamos a configurarlo. Para ello vamos a entrar en el contenedor e instalar un editor de texto.

```bash
docker exec -it wireguard /bin/bash
apt install nano
```
![](/assets/Practica13 VPN/parte2/5.png)

A partir de aquí los pasos son los mismos que los de la [practica anterior.](wireguard-ubuntu2204)

### Conexión
Para está práctica he cambiado tanto la red de la VPN como la de la red interna, para que sea distinta a la anterior.

![](/assets/Practica13 VPN/parte2/7.png)

### Pruba de conexión

![](/assets/Practica13 VPN/parte2/8.png)

### Esquema de IP's


|Máquina| Adaptador Puente | Red Interna | VPN |
| ------------- | ----------- | --- |
| Servidor| 10.1.1.2/8| 192.168.80.1/24 |172.16.0.1/24 |
| Windows| 10.0.0.10/8 | | 172.16.0.10/24   |
| Lubuntu|  |192.168.80.100/24 ||
