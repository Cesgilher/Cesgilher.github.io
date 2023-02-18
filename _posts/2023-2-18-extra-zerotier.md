---
title: (EXTRA)ZeroTier VPN
published: true
---
En esta práctica vamos a Zerotier una vez más, pero para conectar dos redes, con sus hosts incluidos.


### Configuración de Zerotier

Ya que tenemos uan red creada de la [práctica anterior.](zerotier), solo tenemos que conectar nuestras dos máquinas Ubuntu Server a la red.

Para ello vamos a descargar el cliente de Zerotier en ambas máquinas.

```bash	
sudo wget https://download.zerotier.com/debian/pool/main/z/zerotier-one/zerotier-one_1.6.6_amd64.deb
```

![](/assets/Practica13 VPN/Extra/zerotier/1.png)

Una vez descargado, instalamos el paquete.

```bash
sudo dpkg -i zerotier-one_1.6.6_amd64.deb
```
![](/assets/Practica13 VPN/Extra/zerotier/2.png)



Para conectar las máquinas a la red, basta con poner el id de la red que queramos usar, mediante el siguiente comando.

```bash
sudo zerotier-cli join <id_de_la_red>
```

![](/assets/Practica13 VPN/Extra/zerotier/3.png)

De la misma forma, para desconectarnos usariamos el siguiente comando.

```bash
sudo zerotier-cli leave <id_de_la_red>
```
![](/assets/Practica13 VPN/Extra/zerotier/4.png)

Igual que la otra vez, deberemos de acceder a la web de Zerotier y aceptar la conexión de los equipos.

![](/assets/Practica13 VPN/Extra/zerotier/5.png)

Podemos ver que ya han recibido una ip dentro de la red virtual.

![](/assets/Practica13 VPN/Extra/zerotier/6.png)

Y ahora ya podemos probar la conexión entre las dos máquinas.

![](/assets/Practica13 VPN/Extra/zerotier/7.png)



Ahora solo falta configurar la VPN, para que los clientes de las distintas redes, puedan conectarse entre si. Podemos hacerlo tanto desde los servidores, como desde la web de Zerotier. Yo voy a hacerlo de las dos formas para que veáis como se hace.

### Enrutamiento desde los servidores

Para que los servidores sean capaces de enrutarse entre si, basta con añadir una ruta la red interna del otro servidor.

```bash
sudo ip route add <red interna del otro servidor(donde esta el cliente al que queremos llegar)> via <ip del interfaz vpn del otro servidor>
```

![](/assets/Practica13 VPN/Extra/zerotier/8.png)

Si probamos a hacer un ping desde el cliente de la red 1, al de la red 2, veremos que funciona.

![](/assets/Practica13 VPN/Extra/zerotier/9.png)


Vamos a borrar las rutas que hemos creado para que no interfieran con la configuración de la VPN.Y por consiguiente, ya no podremos hacer ping entre los clientes.

![](/assets/Practica13 VPN/Extra/zerotier/10.png)


### Enrutamiento desde la web

Para hacer lo mismo desde la web, basta con ir a la parte de managed routes y añadir las rutas que queramos.

![](/assets/Practica13 VPN/Extra/zerotier/11.png)

Si hacemos un ip route, podemos ver que se han añadido las rutas correctamente.

![](/assets/Practica13 VPN/Extra/zerotier/13.png)

Por lo tanto, volvemos a tener comunicación entre los clientes.

![](/assets/Practica13 VPN/Extra/zerotier/14.png)


### Esquema de IP's

|Máquina| Adaptador Puente | Red Interna | VPN |
| ------------- | ----------- | --- |
| Servidor1| 10.1.1.1/8| 192.168.10.1/24 |172.23.10.142/16 |
| Lubuntu1|  |192.168.10.100/24 ||
| Servidor2| 10.1.1.2/8| 192.168.80.1/24 |172.23.192.98/16|
| Lubuntu2|  |192.168.80.100/24 ||
