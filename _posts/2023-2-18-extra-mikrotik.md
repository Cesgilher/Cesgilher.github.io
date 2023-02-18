---
title: (EXTRA)Mikrotik
published: true
---
En esta práctica vamos a configurar Wireguard desde un router Mikrotik.


### Configuración de Wireguard

Lo primero de todo es instalar Mikrotik en un maquina virtual, yo ya tengo una creada, así que usaré esa.

Para acceder a la interfaz de Mikrotik, basta con poner la ip de la máquina en el navegador o utilizar Winbox.

Una vez dentro de la interfaz, podemos ver que la extension de Wireguard ya está instalada por defecto.

![](/assets/Practica13 VPN/Extra/mikrotik/2.png)

Ahora vamos a crear un nuevo perfil de Wireguard, para ello vamos a la sección de Wireguard y creamos un nuevo perfil. La nombramos como queramos, asignamos el puerto que mas rabia nos dé y le damos a crear. Esto hará que se genere el par de claves del servidor.

![](/assets/Practica13 VPN/Extra/mikrotik/4.png)

Antes de poder conectar nuestro cliente es necesario crear una interfaz de red. Para ello vamos a la sección de interfaces y creamos una nueva interfaz de tipo Wireguard. Ahí es donde definiremos la red que usará la VPN.

![](/assets/Practica13 VPN/Extra/mikrotik/8.png)

Ahora vamos a la sección de Wireguard y añadimos el perfil que acabamos de crear. En la sección de peers, añadimos la configuración del cliente.

![](/assets/Practica13 VPN/Extra/mikrotik/6.png)

Ahora hacemos lo mismo desde el cliente.

![](/assets/Practica13 VPN/Extra/mikrotik/5.png)

### Prueba de conexión

Vamos a intentar realizar un ping desde el cliente a la maquina de la red interna antes de conectar la VPN y ver que no resuelve la ip.

![](/assets/Practica13 VPN/Extra/mikrotik/7.png)

Conectamos el cliente a la VPN y comprobamos que funciona.

![](/assets/Practica13 VPN/Extra/mikrotik/9.png)










### Esquema de IP's


|Máquina| Adaptador Puente | Red Interna | VPN |
| ------------- | ----------- | --- |
| Servidor| 10.10.10.1/8| 192.168.80.1/24 |172.16.50.1/24 |
| Windows|10.0.0.10/8  | |172.16.50.10/24|
| Lubuntu1|  |192.168.80.50/24 ||
