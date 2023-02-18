---
title: (EXTRA)PFSense
published: true
---
En esta práctica vamos a instalar el plugin de Wireguard en un routert PFSensepara conectar dos equipos a traves de internet.


### Instalación de Wireguard en PFSense

Para instalar el plugin de Wireguard en PFSense, basta con ir a la sección de paquetes y buscar el plugin de Wireguard.

![](/assets/Practica13 VPN/Extra/pfsense/1.png)

![](/assets/Practica13 VPN/Extra/pfsense/2.png)


Ahora vamos al apartado de VPN's y creamos una nueva VPN de tipo Wireguard.

![](/assets/Practica13 VPN/Extra/pfsense/16.png)



Le ponemos la descripción que queramos, generamos el par de claves, y guardamos los cambios.

![](/assets/Practica13 VPN/Extra/pfsense/3.png)


Ahora vamos al apartado de interfaces y creamos una nueva con el tipo de interfaz Wireguard.

![](/assets/Practica13 VPN/Extra/pfsense/4.png)

La editamos y asignamos la red que queramos usar para la VPN.

![](/assets/Practica13 VPN/Extra/pfsense/5.png)

Si volvemos al apartado de wireguard, vemos que nuestro tunel ya tiene asignado la nueva interfaz.

![](/assets/Practica13 VPN/Extra/pfsense/6.png)

Ahora vamos a las reglas del firewall y desde la VPN, en mi caso OPT1, creamos una nueva para permitir el trafico de la VPN.

![](/assets/Practica13 VPN/Extra/pfsense/7.png)

Permitimos todo el trafico entrante que sea UDP y vaya al puerto asignado, en mi caso 51820, que es el que usa por defecto Wireguard.

![](/assets/Practica13 VPN/Extra/pfsense/9.png)


Ahora lo de siempre, ir al cliente y configurar un nuevo tunel para que tire de la VPN.

![](/assets/Practica13 VPN/Extra/pfsense/10.png)

Ahora volvemos a la sección de Wireguard y creamos un nuevo peer en nuestro tunel.

![](/assets/Practica13 VPN/Extra/pfsense/11.png)

![](/assets/Practica13 VPN/Extra/pfsense/12.png)




### Prueba de conexión

Con todo conectado podemos ver como los dos equipos se ven entre si.

![](/assets/Practica13 VPN/Extra/pfsense/13.png)

Y como siempre, si desconectamos el tunel, ya no se ven.

![](/assets/Practica13 VPN/Extra/pfsense/14.png)


### Esquema de IP's


|Máquina| Adaptador Puente | Red Interna | VPN |
| ------------- | ----------- | --- |
| Servidor1| 10.1.1.1/8| 192.168.10.1/24 |172.16.50.1/24 |
| Windows| 10.0.0.10/8||172.16.50.10/24 |
| Lubuntu1|  |192.168.10.100/24 ||
