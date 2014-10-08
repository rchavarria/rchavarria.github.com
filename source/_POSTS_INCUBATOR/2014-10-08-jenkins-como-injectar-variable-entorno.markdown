# Cómo inyectar una variable de entorno en un trabajo de Jenkins

un poco de introducción, de porque se necesita y demás

Más concretamente cómo se inyecta la variable PATH

## Requisitos

Se requiere tener instalado en plugin '[Environment Injector Plugin](https://wiki.jenkins-ci.org/display/JENKINS/EnvInject+Plugin)'.

Este plugin añade una nueva sección en la pagina de configuracion de los trabajos de jenkins: *Build Environment*

## Proceso

una vez que ya esta todo:
1. Ir a la ágina de configuracion del trabajo.
2. Localizar la sección *Build Environment*
3. Activar la opcion *Inject environment variables to the build process* (Inyectar variables de entorno en el proceso de construcción).
4. En el campo *Properties Content*, modificar la variable de entorno que necesitamos

%img la imagencita con el text a modificar%

Este ejemplo muestra como se configura un Jenkins instalado en un Linux, en Windows se utilizaría de otra forma ya que las variables de entorno no son exactamente iguales

