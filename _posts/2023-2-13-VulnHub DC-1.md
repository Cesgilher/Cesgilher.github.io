---
title: Vulnhub DC-1
published: true
---
**Resolucion de la maquina DC-1 de Vulnhub**


[Link al ejercicio](https://www.vulnhub.com/entry/dc-1,292/).

Hoy vamos a resolver la Maquina DC-1 de Vulnhub
## Escaneo de puertos

Lo primero es ver que ip tiene la maquina. Para ello vamos a hacer un nmap a la red local.

![](/assets/vulnhub/dc-1/1.png)

Ahora que sabemos que ip tiene la maquina, vamos a realizar un escaneo de puertos con nmap para ver que puertos tenemos abiertos en la maquina.

```bash
nmap -sV -A 10.0.215.87
```

![](/assets/vulnhub/dc-1/2.png)

Vemos que en el puerto 80 tiene un servicio Drupal, concretamente en la versión 7. Así que vamos a usar la herramienta searchsploit para ver si hay alguna vulnerabilidad para esta versión.

```bash
searchsploit drupal 7
```

![](/assets/vulnhub/dc-1/3.png)


Vemos que tiene una vulnerabilidad drupalgeddon2, que nos permite ejcutado codigo de forma remota. Asi que vamos a usar Metasploit para explotar esta vulnerabilidad.

```bash	
msfconsole
set rhost 10.0.215.87
exploit
```

![](/assets/vulnhub/dc-1/4.png)

Hemos accedido a la maquina, ahora vamos a crear una shell para poder movernos por ella.

![](/assets/vulnhub/dc-1/5.png)

Antes de continuar, vamos a importar un interprete /bin/bash para que sea mas comodo trabajar con la shell.

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```

![](/assets/vulnhub/dc-1/6.png)

Si hacemmos un ls dentro del directorio en el que estamos, vemos la primera bandera.

![](/assets/vulnhub/dc-1/7.png)

He intentado acceder al directorio root, pero no podía ser tan fácil. Aun no tenemos permisos.

![](/assets/vulnhub/dc-1/9.png)

Asi que vamos a ver que hay en /home.

![](/assets/vulnhub/dc-1/10.png)

Podemos ver que ahí hay otra bandera. Esta nos da la pista de lo que hay que hacer a continuación. Para ganar permisos de root, vamos a usar el siguiente expliot.

```bash
find . -exec /bin/sh -i \; -quit
```

![](/assets/vulnhub/dc-1/11.png)

Ahora si volvemos al directorio /root, podemos ver la ultima bandera.

![](/assets/vulnhub/dc-1/12.png)

![](/assets/vulnhub/dc-1/13.png)