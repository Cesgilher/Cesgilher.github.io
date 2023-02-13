---
title: Vulnhub DC-1.1
published: true
---
**Resolucion de la maquina DC-1.1 de Vulnhub**


[Link al ejercicio](https://www.vulnhub.com/entry/dc-1,292/).

Hoy vamos a resolver la Maquina DC-1.1 de Vulnhub, la cual es una maquina de Windows Server 2008 R2. La maquina es bastante sencilla, pero es una buena practica para empezar a resolver maquinas de Vulnhub.

## Escaneo de puertos

Para empezar, vamos a realizar un escaneo de puertos con nmap para ver que puertos tenemos abiertos en la maquina.

```bash
nmap -sV -sC -oN nmap/initial
```

![](https://i.imgur.com/0Z7ZQ9M.png)

Vemos que tenemos los puertos 80, 139 y 445 abiertos. Vamos a empezar por el puerto 80, que es el que mas nos interesa.

## Escaneo de servicios

Vamos a realizar un escaneo de servicios con nmap para ver que servicios tenemos corriendo en los puertos que tenemos abiertos.

```bash
nmap -p 80,139,445 -sV -sC -oN nmap/services
```

![](https://i.imgur.com/1Z0ZQ9M.png)

Vemos que tenemos el servicio http corriendo en el puerto 80. Vamos a ver que tenemos en el puerto 139 y 445.

## Escaneo de SMB


```bash
nmap -p 139,445 --script=smb-enum-shares.nse,smb-enum-users.nse -oN nmap/smb
```


![](https://i.imgur.com/2Z0ZQ9M.png)

Vemos que tenemos un usuario llamado "Administrator" y un share llamado "Public". Vamos a ver que tenemos en el share "Public".


```bash
smbclient -L \\\\
```

![](https://i.imgur.com/3Z0ZQ9M.png)

Vemos que tenemos un share llamado "DC-1.1". Vamos a ver que tenemos en el share "DC-1.1".


```bash
smbclient \\\\
```

![](https://i.imgur.com/4Z0ZQ9M.png)

Vemos que tenemos un archivo llamado "DC-1.1.txt". Vamos a ver que tenemos en el archivo "DC-1.1.txt".

## Escaneo de HTTP  (80)

Vamos a ver que tenemos en el puerto 80.

......

