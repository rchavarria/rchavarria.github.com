---
layout: post
title: "Desplegar una aplicación Angular en producción"
date: 2018-10-24 00:00
author: Ruben Chavarria
categories:
- Aprendizaje
- Programación
- Deploy
---

Estoy desarrollando una aplicación que consta de varios sistemas.
No se trata para nada de algo hecho con microservicios, pero el
sistema completo está compuesto de varias aplicaciones. Algunas
del lado servidor, y una applicación web escrita en [Angular].

En estas notas quiero apunta cómo desplegar una applicación Angular
y servirla a través de un servidor HTTP [nginx].

<!-- more -->

## Primer intento

Existen varias formas de servir una aplicación Angular. La primera
de ellas, es un servidor que viene incluido cuando creas tu
aplicación con `angular-cli`. Muy fácil, simplemente tecleas el
comando:

```
npm run serve
```

Y a correr.

Pero ese método, para producción, no es muy bueno. Para desarrollo
sí, porque te detecta los cambios que vas haciendo en tu código y
te recarga la aplicación en el navegador, por lo que automáticamente
vas viendo tus cambios en el navegador.

Para desplegarla en producción hay que generar un *paquete*. En
realidad hay que *construir* varios ficheros JavaScript y un
pequeño fichero HTML que será el inicio de tu aplicación.

Ejecutamos el comando `npm run build` y estos ficheros se crearán
en el directorio `dist`.

Copiando esos ficheros al directorio que sirve tu servidor web
preferido (Apache, nginx,...), ya podrás acceder a tu aplicación
web Angular.

Pero hay un problema, y es que mi aplicación usa **rutas**, lo que
quiere decir es que la URL `/devices/1234` en realidad no es una
URL que obtiene HTML del servidor, si no que es Angular quien la
reconoce y genera el HTML en el lado cliente. Así, si estás en esa
ruta de la aplicación y refrescas la página, obtienes un error
**HTTP 404** como una catedral.

Tardé un tiempo en darme cuenta de ello, y en comprender cuál era
el problema. Era cuestión de leer con más detalle la propia
documentación de Angular...

## Una mejor solución

Pues resulta que la solución se llama *fallback to index.html*
(ver [documentación]).

> If the app uses the Angular router, you must configure the
server to return the application's host page (`index.html`)
when asked for a file that it does not have.

Esta gente de Angular es muy maja e incluye un ejemplo de
configuración para nginx:

```
try_files $uri $uri/ /index.html;
```

Resulta que es un problema bastante conocido y en la documentación
de ngnix lo encontrarás como [Front Controller Pattern Web Apps].

¿Dónde hay que escribir esa línea de configuración?

Parece que funciona perfectamente en la sección `server` de
`/etc/nginx/nginx.conf`:

```
# ...
server {
    listen 80;
    root /var/www/html;

    location /api/ {
        proxy_pass ...
    }

    # fallback to index.html
    try_files $uri $uri/ /index.html;
}
```

## Referencias

- [Front Controller Pattern Web Apps]

[Angular]: https://angular.io
[nginx]: https://nginx.org
[documentación]: https://angular.io/guide/deployment#routed-apps-must-fallback-to-indexhtml
[Front Controller Pattern Web Apps]: https://www.nginx.com/resources/wiki/start/topics/tutorials/config_pitfalls/#front-controller-pattern-web-apps
