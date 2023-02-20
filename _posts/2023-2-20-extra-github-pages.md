---
title: (EXTRA)Github Pages
layout: post
---
En este post vamos a ver como añadir Google Analytics y Disqus a nuestra pagina de GitHub Pages. Aparte de esto, vamos a crear un subdmonio para otro de nuestros repositorios de GitHub.
### Google Analytics

Lo primero es crear una cuenta en Google Analytics. Una vez creada, vamos a la pestaña de administración y creamos un nuevo sitio web.
![](/assets/jekyll/extra/parte1/6.png)
![](/assets/jekyll/extra/parte1/7.png)
![](/assets/jekyll/extra/parte1/8.png)

En la pestaña de seguimiento, seleccionamos la opción de seguimiento universal y copiamos el código que nos proporciona.

![](/assets/jekyll/extra/parte1/5.png)

Pegamos el id en el archivo de configuración de nuestra página de GitHub Pages, que se encuentra en la raíz del repositorio. En nuestro caso, el archivo se llama _config.yml. Si no lo tenemos, lo creamos. El archivo debe tener el siguiente aspecto:

```yml
google_analytics: <id>
```
![](/assets/jekyll/extra/parte1/3.png)

Ahora para que se ejecute el codigo en cada pagina, en _includes creamos un archivo analytics.html con el siguiente contenido:

![](/assets/jekyll/extra/parte1/2.png)

Y en _layouts agregamos las siguientes lienas al archivo default.html:

![](/assets/jekyll/extra/parte1/1.png)

Con esto ya tendriamos Google Analytics funcionando en nuestra pagina de GitHub Pages.

![](/assets/jekyll/extra/parte1/9.png)

### Disqus

Para añadir Disqus a nuestra pagina de GitHub Pages, lo primero es crear una cuenta en Disqus. Una vez creada, vamos a la pestaña de administración y creamos un nuevo sitio web. Yo, cuando fui a enlazar mi cuenta de Google, descubri que ya tenia una cuenta creada hace 8 años, por que debe ser que comente en algun blog que lo usaba.

![](/assets/jekyll/extra/parte2/1.png)

Creamos un nuevo sitio web.

![](/assets/jekyll/extra/parte2/2.png)

Elejimos la plataforma que vamos a usar, en nuestro caso, Jekyll.

![](/assets/jekyll/extra/parte2/4.png)


Ahora en default.html, añadimos el siguiente codigo.

![](/assets/jekyll/extra/parte2/6.png)

Esto hará que los comentarios esten disponibles. Pero para que se muestres deberemos ir a post.html y añadir lo siguiente.

![](/assets/jekyll/extra/parte2/5.png)


Y añadimos el siguiente codigo.

![](/assets/jekyll/extra/parte2/7.png)


Podemos aprobar o eliminar los comentarios que recibamos desde nuestro perfil de Disqus. Y eso es todo, ya tenemos Disqus funcionando en nuestra pagina de GitHub Pages.




### Subdominio

Para crear un subdominio, lo primero es crear un repositorio en GitHub.Una vez creado, vamos a la pestaña de settings y en la sección de GitHub Pages, seleccionamos la opción de usar un dominio personalizado.

![](/assets/jekyll/extra/parte3/1.png)
![](/assets/jekyll/extra/parte3/2.png)
![](/assets/jekyll/extra/parte3/3.png)

Si ahora vamos a la pestaña de settings, en la sección de GitHub Pages, veremos que nos aparece la url de nuestro [subdominio](https://cesgilher.github.io/ASIR22-23).Si este usara algun tema o estilo, podriamos verlo en la url de nuestro subdominio. Pero como no lo usamos, solo se ve loq ue hay en el README.md.



