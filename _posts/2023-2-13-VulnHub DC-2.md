---
title: Vulnhub DC-2
published: true
---
**Resolucion de la maquina DC-2 de Vulnhub**


[Link al ejercicio](https://www.vulnhub.com/entry/dc-2,311/).

Hoy vamos a resolver la Maquina DC-2 de Vulnhub
## Escaneo de puertos

Al igual que en la [maquina anterior](VulnHub-DC-1), lo primero es ver que ip tiene la maquina. Una vez lo hayamos hecho, vamos a realizar un escaneo de puertos con nmap para ver que puertos tenemos abiertos en la maquina.

```bash
nmap -sV -sC -sT -p- 10.0.244.73
```

![](/assets/vulnhub/dc-2/1.png)

Podemos ver como tiene el puerto 80 abierto, asi que vamos a ver que hay en el.

![](/assets/vulnhub/dc-2/5.png)

Cuando intentamos acceder al puerto 80 de la maquina, esta cambia el dominio a dc-2. Al no tener ese nameserver en nuestra maquina, nuestro navegador no es capaz de resolverlo. 

![](/assets/vulnhub/dc-2/6.png)



Pero esto tiene facil solucion, y es que basta con añadir una linea en el fichero hosts de nuestra maquina.

```bash
echo 10.0.244.73 dc-2 >> /etc/hosts
```

![](/assets/vulnhub/dc-2/7.png)

Si intentamos acceder a la maquina ahora, nos encontramos con una pagina basada en wordpress.

![](/assets/vulnhub/dc-2/8.png)

Y encotramos la primera bandera. Desgraciadamente, parece que no podemos seguir por aquí. Lo que si sabemos es que en base a la bandera, hay que usar cewl, una herramienta que nos permite crear diccionarios de palabras a partir de un sitio web.

![](/assets/vulnhub/dc-2/9.png)


Por suerte tenemos otro puerto abierto, el 7744, con un servidor SSH en el.Probablemente para el administrador wed del wordpress. Asi que vamos a usar cewl para crear un diccionario de palabras a partir de la pagina web. Y con suerte una de esas palabras sea la contraseña del usuario.

```bash
cewl -w dc2.txt http://dc-2/
```

![](/assets/vulnhub/dc-2/10.png)

Ahora vamos a probar a hacer un brute force con wpscan para ver si podemos acceder al Webadmin.

```bash
wpscan --url http://dc-2/ --passwords dc2.txt 
```

![](/assets/vulnhub/dc-2/11.png)

![](/assets/vulnhub/dc-2/12.png)


Y vemos como hemos conseguido dos credenciales, una para el usuario jerry y otra para el usuario tom. Vamos a probar a ver si podemos acceder con alguna de ellas.

![](/assets/vulnhub/dc-2/13.png)

Esto es lo que vemos al entrar.

![](/assets/vulnhub/dc-2/14.png)

No hay nada ni en posts ni en comentarios, pero si en paginas, donde tenemos la segunda bandera.

![](/assets/vulnhub/dc-2/15.png)

![](/assets/vulnhub/dc-2/16.png)

Parece que hemos vuelto a otro punto muerto. Ya solo nos queda una opcion, conectarnos directamente por ssh.

```bash
ssh tom@dc-2 -p 7744
```

![](/assets/vulnhub/dc-2/17.png)

Tenemos la tercera bandera.

![](/assets/vulnhub/dc-2/18.png)

Pero no podemos verla porque el interprete es el erroneo. Asi que vamos a probar a cambiarlo.

```bash
vi
:set shell=/bin/bash
:shell
export PATH=/bin/usr/bin:$PATH
export SHELL=/bin/bash:$SHELL
```

![](/assets/vulnhub/dc-2/19.png)

![](/assets/vulnhub/dc-2/20.png)

Ya podemos ver la bandera. Esta nos indica que debemos de logearnos como jerry. Asi que vamos a hacerlo.

![](/assets/vulnhub/dc-2/21.png)

Si vamos al home de jerry, vemos la cuarta bandera.

![](/assets/vulnhub/dc-2/22.png)

Pero ya no tenemos mas pistas, asi que vamos a usar un exploit clasico para escalar privilegios. Y es que vamos a usar el exploit de sudo.

```bash
sudo -l
```

![](/assets/vulnhub/dc-2/23.png)

Ejecutamos el comando git help config como root.

```bash
sudo git help config
```

Dentro del fichero creamos una shell como root.

```bash
!/bin/sh
```

![](/assets/vulnhub/dc-2/24.png)

Y por fin, tenemos la ultima bandera.

![](/assets/vulnhub/dc-2/25.png)

