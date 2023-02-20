---
layout: post
title:  "GitHub Pages con Jeckyll"
published: true
---
En este post vamos a ver como crear una pagina web con GitHub Pages y Jeckyll. Para ello vamos a usar el tema [Hacker Blog](https://github.com/tocttou/hacker-blog). Este no es más que un tema basado en otro publico de GitHub llamado [Hacker](https://github.com/pages-themes/hacker).

## Creación del reposatorio

Lo primero que hay que hacer para crear una pagina web con GitHub Pages es crear un repositorio en GitHub. Para ello vamos a la página de GitHub y creamos un nuevo repositorio, el cual deberá llamarse **usuario.github.io**. En mi caso, el repositorio se llama **cesgilher.github.io**.
Dado que voy a usar el tema mencionado anteriormente, lo que he hecho ha sido hacer un fork del repositorio de este tema y llamar al repositorio **cesgilher.github.io**. De esta forma, si visito la página [https://cesgilher.github.io](https://cesgilher.github.io) veré la página web que he creado. 

## Configuración del repositorio

Una vez creado el repositorio, vamos a un terminal , o a visual studio code, y clonamos el repositorio.

```git
git clone https://github.com/Cesgilher/Cesgilher.github.io
```


 Una vez clonado, vamos a la carpeta del repositorio y abrimos el archivo **_config.yml**. En este archivo vamos a configurar la página web. En mi caso, he cambiado el titulo, el autor, la descripción, el email, el dominio, etc. Ahí es también donde deberemos cambiar la paginación.

![](/assets/jekyll/1.png)

Luego en cuanto al estilo, he cambiado un poco los colores. Esto se hace dentro del archivo _sass/_default_colors.scss y _sass/base.scss.Entre ellos ha cambiado el color de los titulos y el de los enlaces. Además Para que las listas se vean con las felchitas así ">>", he tenido que editar la foto que se utilizaba, ya que por defecto era de color verde.
![](/assets/bullet.png)
![](/assets/bullet.png)
![](/assets/bullet.png)
![](/assets/bullet.png)


![](/assets/jekyll/2.png)




