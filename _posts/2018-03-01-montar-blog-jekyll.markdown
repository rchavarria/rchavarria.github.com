---
title: "Montar un blog con Jekyll"
categories:
- Proyectos
---

El objetivo es poder montar un blog, un sitio web estático o una *landing page* sobre Jekyll. 
Para no guarrear la máquina de desarrollo, se utilizará un contenedor Docker donde ya esté instalado
Jekyll y ruby.

La web estática puede tener muchos usos: escaparate de una empresa, agrupcación de notas como
esta,...

<!-- more -->

## Tecnologías

- [ruby](https://www.ruby-lang.org/en/)
- [Jekyll](https://jekyllrb.com/)
- [Docker](https://www.docker.com/)
- [Docker compose](https://docs.docker.com/compose/): es un amigo genial para Docker y para la falta
de memoria. Ayuda a no tener que recordar con qué comando `docker` hay que crear el contenedor.

## Elegir un tema de Jekyll

1. [Airspace](https://github.com/ndrewtl/airspace-jekyll): este diseño está muy curioso.
Ver [ejemplo](http://www.devempathybook.club/).
2. [Landing page](http://www.jekyllthemes.io/theme/24792726/landing-page-theme): este
también está bien. Es sencillo, pero es resultón, con unas pocas imágenes podría quedar bien.
El [ejemplo](http://shaneweng.com/landing-page-theme/) se ve sencillo y simple.
3. [Agency](https://y7kim.github.io/agency-jekyll-theme/): este también está muy bien, me
gusta mucho los círculos conectados donde cada círculo es un año (como un línea del tiempo
o algo así). A lo mejor exactamente igual no es lo que podría ir bien, pero está curioso.
Ver [ejemplo](https://y7kim.github.io/agency-jekyll-theme/).
4. [One page wonder](https://www.jekyllthemes.io/theme/34391076/one-page-wonder-jekyll):
este diseño quizá es muy simplón. En el
[ejemplo](https://mushishi78.github.io/one-page-wonder-jekyll/), el problema que tiene,
es que como no ponen imágenes, queda muy soso.
5. [Grayscale](https://www.jekyllthemes.io/theme/30191476/grayscale-theme): no está mal
del todo, pero quizá quede muy oscuro

## Levantar el blog con el tema elegido

Muy bien, vamos a utilizar el tema *Airspace*.

Lo primero que hay que hacer es clonar el repositorio con el código fuente del tema:

```
git clone https://github.com/ndrewtl/airspace-jekyll
```

El comando crea un directorio llamado `airspace-jekyll`. Desde ese directorio, levantaremos el blog
a través de un comando `docker-compose`. Pero antes, necesitamos el fichero para dicha
herramienta.

El fichero de configuración de `docker-compose` es un fichero `.yml` donde se pueden configurar
prácticamente todos los parámetros para crear un contenedor. El fichero utilizado es similar
a éste (para ver la última versión, echar un vistazo a este
[repo](https://github.com/rchavarria/web-server-jose/blob/master/docker-compose-master.yml). El
fichero se llamará `docker-compose.yml` para simplificar el proceso:

```
version: '3'

services:
  # a container to serve the blog
  blog:
    image: jekyll/jekyll   # build from latest jekyll
    container_name: blog
    ports:
      - 4000:4000          # expose this port
    volumes:
      - .:/srv/jekyll      # share local source files with the container
      - ./vendor/bundle:/usr/local/bundle     # cache ruby gems
      
    entrypoint:
      - jekyll
      - serve
```

Con él, se indica a `docker-compose` que cree un contenedor (o `service`) llamado `blog`,
a partir de la imagen `jekyll/jekyll` (imagen con la última versión de Jekyll), que exponga
el puerto `4000` y que mapee un par de directorios del sistema host al sistema ^*dockerizado*
(`volumes`). Como último paso, se debe ejecutar el comando (o `entrypoint`) `jekyll serve`.

Otros comandos que se pueden ejecutar serían:

- `bundle install`: para instalar las gemas de ruby necesarias para ejecutar el blog. Aunque
este paso ya se hace automáticamente, puede servir para ir depurando y averiguar si tenemos
algún problema con alguna gema en particular
- `jekyll build`: para construir el blog, generar los ficheros estáticos, pero no servirlos
todavía. Igual que el comando anterior, ya se ejecuta automáticamente con `jekyll serve` pero
puede servir para depurar.

En definitiva, para tener el blog corriendo en local, basta con teclear:

```
cd airspace-jekyll
sudo docker-compose docker-compose.yml
```

Ya tenemos el blog ejecutándose, ahora llega la hora de personalizarlo a nuestro gusto e ir añadiendo
posts

## Estudiando la organización de ficheros del tema

Para poder saber qué debemos personalizar, entendamos primero la organización de los ficheros
del tema:

Comenzaremos por `_config.yml`, porque es el fichero que configura todos los proyectos Jekyll. En él
encontramos los siguientes valores a configurar:

- `title` y `subtitle`
- `url`: será la URL a través de la cual accederán a nuestra web
- `baseurl`: parte de la URL que se añadirá a `url` para completar la ruta a nuestra web. Puede
ser simplemente `""` para indicar que la web estará servida desde el directorio raiz
- `cover` y `logo`: diversas imágenes
- `markdown`: motor de parseo de Markdown
- `descriptions` (lista de `cat` y `desc`): para enumerar cada categoría y sus descripciones
para los posts del blog

Mirando las imágenes incluidas en el tema Airspace, `img/slider-bg.jpg` parece interesante,
ya que es la imagen que aparece en todas las Páginas de la web del tema. Al cambiar esa
imagen se actualiza la primera imagen de fondo que aparece en la página principal.

### Editando las Páginas de Jekyll

El tema original viene con 5 páginas: home, work, blog, service y contact. La idea es dejar
solamente home, y contact.

Los enlaces a esas páginas aparecen en la cabecera. Y resulta que hay un fichero que se llama
`_includes/header.html`. Bingo! En él aparece un código similar a:

```
<ul class="nav navbar-nav navbar-right">
  <li><a href="{{ site.baseurl }}/">Home</a></li>
  <li><a href="{{ site.baseurl }}/work">Work</a></li>
  <li><a href="{{ site.baseurl }}/blog">Blog</a></li>
  <li><a href="#">Service</a></li>
  <li><a href="{{ site.baseurl }}/contact">Contact</a></li>
</ul>
```

En el directorio raíz, también hay unos *misterosos* ficheros llamados: `index.html`
(home), `work.html`, `blog.html`,...

Toca editar `_includes/header.html` y borrar algún fichero en el directorio raíz.

### Página principal

La página principal podría servir como una *landing page*. Tiene varias secciones,
fácilmente identificables en el código HTML gracias a los comentarios del autor del
tema.

1. Slider: foto inicial y más llamativa de la página principal (la editada en
`img/slider-bg.jpg`). Aquí podría ir el título de la empresa
2. Intro: una pequeña introducción de la empresa podría ir aquí
3. Feature: más texto. Lo mejor de esta sección es que también tiene una imagen de
fondo y tiene un efecto de scroll bastante chulo. Habría que mantenerla, pero a ver
qué texto meto aquí
4. Services: una pequeña descripción con un icono de cada uno de los servicios que
proporciona la empresa
5. Call to action: pequeño texto con imagen de fondo difuminada. Podría contener un
botón que llevara a la página de contacto
6. Testimonial: sección con varios efectos visuales pero que creo que se podría
eliminar para la web que llevo en mente

Los estilos CSS de las secciones de la página principal se encuentran en
`css/airspace.css`. Ahí se pueden editar los estilos de cada una de las secciones. De
hecho se ha corregido la ruta a una imagen de fondo que tenía un typo
(`featue` -> `feature`).

### Pie de página

El *footer* también habría que editarlo, porque contiene links a páginas que no
existen y que quizá no tenga mucho sentido mantener. Además del aviso de copyright.

Esta parte tiene toda la pinta de que se puede editar en el fichero
`_includes/footer.htlm`.

## Publicarlo en GitHub Pages

GitHub puede publicar un sitio web Jekyll como una [GitHub Page](https://pages.github.com/).
En teoría es sencillo. A ver si puedo configurarla para que publique un directorio
particular presente en la rama `master`.

Pues sí, es fácil

> Click on the Settings tab and scroll down to the GitHub Pages section.
Then select the master branch source and click on the Save button.

En la pestaña de configuración, ir a la sección de *GitHub Pages*. Elegir la opción a
publicar que más convenga: publicar la carpeta `docs`.

**Problema**

Al publicarlo en GitHub Pages, todos los estilos se pierden. Puede que sea el `baseurl` que
está mal configurado. Puede que el `baseurl` tenga que ser el nombre del repositorio de
GitHub donde está almacenado el site, porque la URL `<mi cuenta de github>/<repo>/<baseurl>`
no muestra nada.

Solución: cambiar la propiedad `baseurl` en `_config.yml` para que coincida con el nombre
del repositorio de GitHub desde donde la web va a ser servida.

## Personalizar página 404

Siguiendo las instrucciones de la [ayuda](https://help.github.com/articles/creating-a-custom-404-page-for-your-github-pages-site)
se puede configurar muy fácilmente. Simplemente crear un fichero `404.html` en la raiz de
la web y configurar la propiedad `permalinkp` en la cabecera del fichero (todos los ficheros
servidos por Jekyll deben tener una cabecera, *front matter* le llama Jekyll).

## Usar un dominio propio

## ¿Qué mas?

## Referencias

- [Jekyll + Docker + Github Pages](http://cowsandcode.com/2018/jekyll-docker-github-pages/):
de aquí surgió la idea original de este proyecto. No he seguido los pasos uno por uno, he
tenido que improvisar e investigar por mi cuenta, pero eso no le quita mérito al post.
- [Using a custom domain with GitHub Pages](https://help.github.com/articles/using-a-custom-domain-with-github-pages/):
cómo usar un dominio propio para ser servido por GitHub Pages
- [GitHub Pages avanzadas](https://help.github.com/articles/further-reading-on-github-pages/)

