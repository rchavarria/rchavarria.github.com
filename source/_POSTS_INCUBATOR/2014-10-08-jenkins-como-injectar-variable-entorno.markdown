# Cómo inyectar una variable de entorno en un job de Jenkins

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
'[Environment Injector Plugin]'. Este plugin añade una nueva sección en la pagina de configuracion de los trabajos de jenkins: *Build Environment*

## Proceso

una vez que ya esta todo:
1. Ir a la ágina de configuracion del trabajo.
2. Localizar la sección *Build Environment*
3. Activar la opcion *Inject environment variables to the build process* (Inyectar variables de entorno en el proceso de construcción).
4. En el campo *Properties Content*, modificar la variable de entorno que necesitamos

%img la imagencita con el text a modificar%

Este ejemplo muestra como se configura un Jenkins instalado en un Linux, en Windows se utilizaría de otra forma ya que las variables de entorno no son exactamente iguales

[Jenkins]: http://www.jenkins-ci.org
[Environment Injector Plugin]: https://wiki.jenkins-ci.org/display/JENKINS/EnvInject+Plugin
