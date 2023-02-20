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

## Configuración del tema
Luego en cuanto al estilo, he cambiado un poco los colores. Esto se hace dentro del archivo _sass/_default_colors.scss y _sass/base.scss.Entre ellos ha cambiado el color de los titulos y el de los enlaces. Además Para que las listas se vean con las felchitas así ">>", he tenido que editar la foto que se utilizaba, ya que por defecto era de color verde.
![](/assets/bullet.png)


![](/assets/jekyll/2.png)

Ademas, he cambiado el logo de la página web. Para ello, he usado una IA como MidJourney. Esta IA me ha creado un logo a partir de una imagen que le he dado. El logo que he creado es el siguiente:

![](favicon.png)

Para añadirlo a mi web, he tenido que editar el archivo **_includes/head.html** y añadir el siguiente código:

```html
<link rel="icon" type="image/png" href="/favicon.png">
```
![](/assets/jekyll/3.png)

Los posts se crean en la carpeta **_posts**. Para crear un post, hay que crear un archivo con el formato **AAAA-MM-DD-nombre-del-post.md**. Por como esta configurado el tema, estó hara que la pagina por defecto sea una pagina con los posts ordenados por fecha descendente. En funcion del numero que hayamos establecido en la configuración, se mostrarán un numero de posts por pagina. En mi caso, he establecido que se muestren 3 posts por pagina.

![](/assets/jekyll/4.png)

Para ver los post creados, bien podemos ir a la pagina principal. O bien, ir a publicaciones donde se muestran todos los posts.


### Añadir imagenes

Todas las imagenes usadas son estaticas, es decir, no se generan dinamicamente. Para añadir una imagen, hay que añadirla a la carpeta **assets** y luego añadirla al post con el siguiente código:

```markdown
![](/assets/nombre-de-la-imagen.png)
```
# Tablas
Para crear una tabla que salga de un listado, hay que crear un archivo .json dentro de la carpeta _data, donde meter un array de objetos. En mi caso, voy a crear el archivo jekyll.json con el siguiente contenido:

```json
[
    { "nombre": "Lunes", "numero": 1 },
    { "nombre": "Martes", "numero": 2 },
    { "nombre": "Miércoles", "numero": 3 },
    { "nombre": "Jueves", "numero": 4 },
    { "nombre": "Viernes", "numero": 5 },
    { "nombre": "Sábado", "numero": 6 },
    { "nombre": "Domingo", "numero": 7 }
  ]
```
Luego, en el post, hay que añadir el siguiente código:

![](/assets/jekyll/5.png)

Y aquí tenemos el resultado:
<table>
    <tr>
    <th>Día de la semana</th>
    <th>Día del mes</th>
    </tr>
    {% for dia in site.data.jekyll %}
    <tr>
    <td>{{dia.nombre}}</td>
    <td>{{dia.numero}}</td>
    </tr>
    {% endfor %}
</table>


### Colecciones

Para crear una colección hay que crear una carpeta de tipo _'nombre-de-la-coleccion'_ y dentro de ella crear archivos .md con el siguiente contenido:

```markdown
---
title: "Nombre del post"
---
Contenido del post
```

![](/assets/jekyll/6.png)

Yo he creado estos tres.

![](/assets/jekyll/9.png)

Una vez creados los distintos elementos de la colección, vamos a crear una nueva plantilla en layouts, realmenta da igual como se llame esta, pero siempre es mejor llamarla igual que nuestra colección para no liarnos. En esta añadiremos el siguiente código:

![](/assets/jekyll/7.png)

Ahora desde nuestro _config.yml, vamos a añadir la siguiente linea:

```yml
collections:
  coleccion:
    output: true
```
![](/assets/jekyll/8.png)

El output: true es para que se genere la pagina una pagina por cada item de la colección. Si lo ponemos a false, solo se generará una pagina con todos los items de la colección.

Ahora creamos un archivo nuevo en la carpeta raiz del proyecto, y añadimos el siguiente código:

```markdown
---
layout: coleccion
title: "titulo de la pagina"
---
```

Yo lo he vinculado en el menu de la pagina principal, de forma que si vamos a Links de interes, nos llevará a la pagina con la [colección](/links).

![](/assets/jekyll/10.png)

### Subir la pagina a GitHub Pages	

Si aun no hemos creado el workflow de jekyll, lo primero sera hacer un push al repositorio. Y una vez actualizados los cambios, vamos a ajustes del repositorio y activamos GitHub Pages. Es bastante sencillo la verdad.

![](/assets/jekyll/11.png)

Y esperamos a que se genere la pagina. En mi caso, depende del momento, ha tardado mas a menos. Pero en general, no ha tardado mas de 5 minutos.
Cuando veamos esto en la pagina, ya estará todo listo, y podriamos ir a nuestro dominio y ver la pagina.

![](/assets/jekyll/12.png)

### Subir la pagin a Netlify

Para subir la pagina a Netlify, lo primero que tenemos que hacer es crear una cuenta en Netlify. Una vez creada la cuenta, vamos a la pagina principal y seleccionamos el repositorio que queremos subir. En mi caso, he seleccionado el repositorio de la pagina de jekyll.

Yo no se si es por algun plugin o qué. Pero tuve que añadir el archivo .ruby-version con la versión que uso en mi proyecto.

![](/assets/jekyll/13.png)

Segun he [leido](https://www.netlify.com/blog/2017/05/11/migrating-your-jekyll-site-to-netlify/), esto es para que Netlify sepa que version de ruby usar. Ya que por defecto, usa la 2.4.3, y yo he usado otra. Y algunos plugins no estan disponibles en la 2.4.3. Lo demas es bastante similar a github, si no tenemos ningun problema, la pagina se subirá sola cada vez que hagamos un push.




