---
title: Conectar dos redes mediante Wireguard VPN
published: true
---
En esta práctica vamos a usar Wireguard para conectar dos redes.

### Configuración de Wireguard

Para está práctica vamos a utilizar las máquinas de las dos prácticas anteriores.

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
| Lubuntu1|  |192.168.80.100/24 ||
