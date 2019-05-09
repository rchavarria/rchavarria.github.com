---
title: "Jenkins CI: inyectar variable de entorno"
date: 2014-10-17 08:44
author: Rubén Chavarría
comments: true
categories: 
- Jenkins
- Continuous Integration
published: true
footer: false
sidebar: true
---

Recientemente, me ha surgido la necesidad de inyectar, o modificar más bien, una
variable de entorno en el servidor de integración contínua que usamos en el
trabajo, [Jenkins].

Uno de los *jobs* de Jenkins necesita una aplicación recientemente instalada, y
dicha aplicación no está alojada en ningún directorio definido dentro de la
variable de entorno `PATH`. Por lo cual, el *job* fallaba.

Una posible solución a este problema era el de modificar la variable de entorno
a nivel global, pero eso podría entrar en conflicto con otros *jobs*. Por lo cual
decidí cambiarla sólo a nivel de *job*. Por lo que llegamos a la pregunta:
¿Cómo se inyecta una variable de entorno en un *job* de Jenkins?

<!-- more -->

## Requisitos

Para poder hacerlo se requiere tener instalado en plugin
'[Environment Injector Plugin]'. Este plugin añade una nueva sección en la página
de configuracion de los trabajos de jenkins: *Build Environment*.

## Proceso

Una vez que el plugin está instalado, seguir estos sencillos pasos:

1. Ir a la página de configuración del trabajo.
2. Localizar la sección *Build Environment*.
3. Activar la opcion *Inject environment variables to the build process* (Inyectar
variables de entorno en el proceso de construcción).
4. En el campo *Properties Content*, modificar la variable de entorno que necesitamos.

En la siguiente imagen se puede ver el texto necesario para inyectar la variable
`PATH` en un entorno Linux. A dicha variable le estoy añadiendo una ruta donde
se encuentra la aplicación que necesita el *job* que estoy configurando.

![Jenkins build environment]({{ site.baseurl }}/assets/images/2014/jenkins-build-environment.png)

Este ejemplo muestra como se configura un Jenkins instalado en un Linux, en
Windows se utilizaría de otra forma ya que las variables de entorno no
son exactamente iguales, así como la configuración de las mismas.

[Jenkins]: http://www.jenkins-ci.org
[Environment Injector Plugin]: https://wiki.jenkins-ci.org/display/JENKINS/EnvInject+Plugin
