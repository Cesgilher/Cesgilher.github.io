---
title: (EXTRA)OpenVPN
published: false
---
En esta práctica vamos a usar Zerotier para conectar dos equipos a traves de internet.

Para simular esto, usaremos un equipo windows conectado a internet y un movil con 5G.

### Configuración de Zerotier

Lo primero de todo es crearnos una cuenta en la web de zerotier, si no la tenemos ya creada. Puedes vincular tu cuenta de GitHub.

![](/assets/Practica13 VPN/parte4/1.png)

Una vez creada la cuenta, vamos a la sección de networks y creamos una nueva red.

![](/assets/Practica13 VPN/parte4/2.png)


Ahora basta con descargar el cliente de Zerotier tanto en windows como en el movil y conectarnos. Es tan sencillo como poner el id de la red que acabamos de crear y listo, ya estaría configurada la VPN. 

![](/assets/Practica13 VPN/parte4/3.png)
![](/assets/Practica13 VPN/parte4/6.png)

Destacar que para que funcione en el movil usando 5G, es necesario permitir su uso.

![](/assets/Practica13 VPN/parte4/7.png)
![](/assets/Practica13 VPN/parte4/8.png)

Ahora basta con volver a la web de Zerotier y permitir la conexión a los equipos.

![](/assets/Practica13 VPN/parte4/4.png)

### Prueba de conexión

#### Windows a movil
![Windows a movil](/assets/Practica13 VPN/parte4/5.png)

#### Movil a Windows

![Windows a movil](/assets/Practica13 VPN/parte4/9.png)
![Windows a movil](/assets/Practica13 VPN/parte4/10.png)
![Windows a movil](/assets/Practica13 VPN/parte4/11.png)





<!-- Para está práctica vamos a u0tilizar las máquinas de las dos prácticas anteriores.

- [parte 1](wireguard-ubuntu2204)
- [parte 2](wireguard-docker)

Dado que ya tenemos Wireguard instalado en ambas máquinas, vamos a configurar la VPN. Para ello basta con poner la configuración de cada servidor, como peer del otro.

![](/assets/Practica13 VPN/parte3/1.png)

Si activamos la vpn en ambas máquinas, y usamos el comando wg, podemos ver que están conectadas exitosamente.

![](/assets/Practica13 VPN/parte3/2.png)

### Prueba de conexión

Para ver que no hay trampa alguna, vamos a realizar un intento de ping entre los dos clientes para ver que no funciona.

![](/assets/Practica13 VPN/parte3/3.png)

Ahora vamos a ver que pasa si activamos la VPN en ambas máquinas.

![](/assets/Practica13 VPN/parte3/4.png)

Como podemos ver, ahora sí es capaz de llegar a la maquina destino volver con los correspondientes echo reply.

### Esquema de IP's


|Máquina| Adaptador Puente | Red Interna | VPN |
| ------------- | ----------- | --- |
| Servidor1| 10.1.1.1/8| 192.168.10.1/24 |172.16.0.1/24 |
| Lubuntu1|  |192.168.10.100/24 ||
| Servidor2| 10.1.1.2/8| 192.168.80.1/24 |172.16.0.2/24 |
| Lubuntu1|  |192.168.80.100/24 || -->
