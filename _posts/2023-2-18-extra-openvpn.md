---
title: (EXTRA)OpenVPN
published: True
---
En esta práctica vamos a usar OpenVPN para conectar dos equipos a traves de internet.

Se puede instalar en Windows, linux, docker y varios routers como Mikrotik o PFSense. Yo voy a utilizar PFSense porque me parece bastante fácil de configurar, además de porque la extension de OpenVPN viene instalada por defecto en PFSense.
### Configuración de OpenVPN

Lo primero de todo es crear una CA dentro de PFSense. Para ello vamos a System->Certificate Manager->CAs y creamos una nueva CA.

![](/assets/Practica13 VPN/Extra/openvpn/3.png)

Le ponemos el nombre que queramos y le damos a save.

![](/assets/Practica13 VPN/Extra/openvpn/4.png)

![](/assets/Practica13 VPN/Extra/openvpn/5.png)

Ahora en la pestaña de Certificados, creamos uno nuevo para el servidor.

![](/assets/Practica13 VPN/Extra/openvpn/7.png)

Hay que asegurarnos de que el certificado sea de tipo Servidor.

![](/assets/Practica13 VPN/Extra/openvpn/8.png)

Si todo ha ido bien, deberíamos tener algo así.

![](/assets/Practica13 VPN/Extra/openvpn/9.png)

Ahora vamos a System->User Manager y creamos un nuevo usuario.

![](/assets/Practica13 VPN/Extra/openvpn/10.png)

Si queremos que además de contraseña, use un certificado, vamos a la parte de User Certificate y creamos uno nuevo, esto nos redirigirá a la pestaña de certificados donde deberemos crear uno nuevo, pero esta vez de tipo Cliente.

![](/assets/Practica13 VPN/Extra/openvpn/11.png)

![](/assets/Practica13 VPN/Extra/openvpn/12.png)

Si todo ha ido bien, ahora en la configuración del usuario, deberíamos tener algo así.

![](/assets/Practica13 VPN/Extra/openvpn/13.png)



### Configuración de la VPN

Ahora vamos a VPN->OpenVPN->Server y creamos una nueva configuración. Aquí definiremos la red, el puerto, el protocolo, etc. Además de el tipo de seguridad que queremos que tenga la VPN. En mi caso voy a usar TLS + User Auth.

![](/assets/Practica13 VPN/Extra/openvpn/15.png)

En la parte de configuración cryptográfica, vamos a poner el certificado que acabamos de crear.Y estableceremos el tipo de encriptación que queremos usar. Si no habeis cambiado nada en los pasos anteriores, no hace falta ni que la toquéis.

![](/assets/Practica13 VPN/Extra/openvpn/16.png)

En la parte de ajustes de tunel, es donde deberemos poner la red que queremos que sea la VPN, ademas de las rutas que queremos que se usen.

![](/assets/Practica13 VPN/Extra/openvpn/17.png)

En la parte del cliente no hace falta cabiar nada, y en configuración avanzada, elegir si queremosa que cree una puerta de enlace para IPv4, IPv6 o ambas. En mi caso solo voy a usar IPv4.

![](/assets/Practica13 VPN/Extra/openvpn/19.png)

Si guardamos los cambios y vamos a Status->OpenVPN, deberíamos ver que la VPN está activa.

![](/assets/Practica13 VPN/Extra/openvpn/20.png)

### Configuración del firewall

Ya tenemos nuestra Vpn creada y corriendo, pero si queremos que funcione, tenemos que configurar el firewall para que permita el trafico de la VPN. Para ello vamos a Firewall->Rules->OpenVPN y creamos una nueva regla.

![](/assets/Practica13 VPN/Extra/openvpn/22.png)

Ahora vamos a Firewall->Rules->WAN y creamos una nueva regla, para permitir la conexión al puerto que hemos elegido para la VPN.

![](/assets/Practica13 VPN/Extra/openvpn/23.png)

![](/assets/Practica13 VPN/Extra/openvpn/24.png)

### Descarga del cliente

Bien podriamos instalar el programa de OpenVPN en el equipo cliente, pero en este caso vamos a usar una extension de PFSense, que nos permite crear un instalador personalizado, con la configuración que queramos. Para ello vamos a instalar la extension.

![](/assets/Practica13 VPN/Extra/openvpn/25.png)

Una vez instalada, vamos a VPN->OpenVPN->Client Exporter y creamos una nueva configuración.

![](/assets/Practica13 VPN/Extra/openvpn/26.png)

Lo que mas me gusta de esta extension, es que es compatible con la mayoria de dispositivos y sistemas operativos. En mi caso voy a usar Windows, pero podriamos usar Android, iOS, Linux, MacOS, etc.

![](/assets/Practica13 VPN/Extra/openvpn/27.png)

Una vez creado el instalador, lo descargamos y lo ejecutamos. Esto iniciará un wizard de instalación para OpenVPN. 

Después, ya solo tendremos que conectarnos a la VPN y listo. Nos pedirá el usuario y contraseña que creamos en el paso anterior.

![](/assets/Practica13 VPN/Extra/openvpn/28.png)

![](/assets/Practica13 VPN/Extra/openvpn/29.png)

Y como se puede ver a continuación, ya tenemos acceso a la red de la VPN.

![](/assets/Practica13 VPN/Extra/openvpn/30.png)

### Prueba de Ping  

![](/assets/Practica13 VPN/Extra/openvpn/31.png)

Si desconectamos la VPN, ya no podremos acceder a la red interna.

![](/assets/Practica13 VPN/Extra/openvpn/32.png)

### Esquema de IP's


|Máquina| Adaptador Puente | Red Interna | VPN |
| ------------- | ----------- | --- |
| Servidor1| 10.0.55.50/8| 192.168.10.1/24 |172.16.77.1/24 |
| Windows| 10.0.0.10/8| |172.16.77.2/24(DHCP)|
| Lubuntu1|  |192.168.80.50/24 ||
