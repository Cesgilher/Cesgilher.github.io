---
title: Instalar Wireguard VPN en Ubuntu Server 22.04
published: true
---
En esta practica voy a explicar el proceso para configurar Wireguard VPN en Ubuntu Server 22.04

### Instalación de Wireguard

Lo primero como siempre en ubuntu es actualizar los repositorios y actualizar el sistema.

```bash
sudo apt update
sudo apt upgrade
sudo apt install wireguard
```
![](/assets/Practica13 VPN/parte1/1.png)

### Configuración del servidor

Una vez instalado, vamos a crear el par de claves para el servidor.

```bash
sudo wg genkey | sudo tee /etc/wireguard/privatekey | sudo wg pubkey | sudo tee /etc/wireguard/publickey
```
Esto generará la clave privada y la clave publica correspondiente a esta. Y las almacena en la carpeta de wireguard para que sean mas accesibles durante el resto del proceso.

![](/assets/Practica13 VPN/parte1/2.png)

Antes de seguir vamos a activar el bit de forwarding en el kernel de linux. Para ello vamos a editar el archivo de configuración del kernel.

```bash
sudo nano /etc/sysctl.conf
```
Y añadimos la siguiente linea.

```bash
net.ipv4.ip_forward=1
```
![](/assets/Practica13 VPN/parte1/4.png)

Ahora vamos a crear el archivo de configuración del servidor. Para ello vamos a crear un archivo de configuración en la carpeta de wireguard.

```bash
sudo nano /etc/wireguard/wg0.conf
```
Dentro de este archivo vamos a añadir la siguiente configuración.

```bash
[Interface]
Address = <una ip dentro de la red que queramos que use la vpn>
SaveConfig = true
ListenPort = <puerto que queramos que use la vpn, por defecto el 51820>
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o <interfaz de salida> -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o <interfaz de salida> -j MASQUERADE
PrivateKey = <clave privada del servidor>
```

![](/assets/Practica13 VPN/parte1/3.png)



Ahora vamos a crear el archivo de configuración del cliente. Para ello vamos a nuestro cliente y en caso de que sea windows, mediante el porgrama de wireguard, vamos a crear un nuevo tunel vacio. En caso de ser linux, vamos a crear un archivo de configuración en la carpeta de wireguard. Aqui vamos a añadir la siguiente configuración.
    
    ```bash
    [Interface]
    Address = <una ip dentro de la red que queramos que use la vpn>
    PrivateKey = <clave privada del cliente>
    [Peer]
    PublicKey = <clave publica del servidor>
    Endpoint = <ip del servidor>:<puerto>
    AllowedIPs =<las ips que queramos que suministre el servidor, en mi caso queremos llegar a la maquina que está en la 192.168.10.100 asi que pondremos 192.168.10.0/24>
    ```

![](/assets/Practica13 VPN/parte1/8.png) 

De vuelta en el servidor, vamos a añadir la siguiente configuración al archivo de configuración del servidor.

```bash
[Peer]
PublicKey = <clave publica del cliente>
AllowedIPs = <la ip que hayamos puesto en el archivo de configuración del cliente>
```

![](/assets/Practica13 VPN/parte1/9.png)

Para que todo esto funcione, vamos a abrir el puerto en el servidor.

```bash
sudo ufw allow <puerto>
```
![](/assets/Practica13 VPN/parte1/5.png)

En caso de que quisieramos que la vpn se arranque con el sistema, hariamos un enable.

![](/assets/Practica13 VPN/parte1/6.png)

Aunque para la practica basta con un start.

![](/assets/Practica13 VPN/parte1/7.png)

Ahora ya podemos activar la vpn.

```bash
sudo wg-quick up wg0
```
![](/assets/Practica13 VPN/parte1/10.png)

Y comprobar que funciona.

![](/assets/Practica13 VPN/parte1/11.png)

En la imagen anterior, se puede ver como el ping no funciona cuando no estamos conectados a la vpn, pero si funciona cuando lo estamos.


### LIsta de iptables utilizadas

```bash    
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT DROP

#SSH
iptables -A INPUT -p tcp --dport 22 -s 10.0.0.10/32 -j ACCEPT
iptables -A OUTPUT -m state --state  established  -d 10.0.0.10/32 -j ACCEPT

#Para permitir la comunicación entre windows y la maquina de la red interna
iptables -A INPUT -p udp --dport 51820 -s 10.0.0.10/32 -j ACCEPT
iptables -A INPUT -i lo -j ACCEPT

iptables -A FORWARD -i <interfaz_vpn> -o <interfaz_interna> -d 192.168.10.100 -j ACCEPT
iptables -A FORWARD -i <interfaz_interna> -o <interfaz_vpn> -s 192.168.10.100 -j ACCEPT

iptables -A OUTPUT -o lo -j ACCEPT
```
### Esquema de IP's


|Máquina| Adaptador Puente | Red Interna | VPN |
| ------------- | ----------- | --- |
| Servidor| 10.1.1.1/8| 192.168.10.1/24 |172.16.10.1/24 |
| Windows| 10.0.0.10/8 | | 172.16.10.10/24   |
| Lubuntu|  |192.168.10.100/24 ||
