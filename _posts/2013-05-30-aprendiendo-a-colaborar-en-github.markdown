---
title: "Aprendiendo a colaborar en github"
date: 2013-05-30 08:45
comments: true
categories: 
- git
- learning
- tools
published: true
footer: false
sidebar: true
---

Recientemente, hablando con mi amigo [David](http://twitter.com/dagarfol) sobre un 
proyectillo que llevamos a medias (estamos empezando, espero que podamos tener algo
publicable pronto), salió el tema de cómo empezar a colaborar con 
amigos/compañeros/quien-sea con [git](http://git-scm.com/) en [github](http://github.com). 

Yo le comenté que era bastante sencillo comenzar, pero de boquilla se pueden decir
muchas cosas (la mayoría mentira), así que para que no se quede en agua de borrajas, 
en este post encontrarás 5 comandos y acciones básicas para comenzar a 
trabajar en equipo con git y github.

<!-- more -->

## ¿Qué necesito?

Lo primero que se necesita es tener una cuenta en github. Si no tienes una, uno puede
[registrarse](https://github.com/users) fácilmente. Es como crearse una cuenta de correo.

![GitHub overview]({{ site.baseurl }}/assets/images/2013/github-overview.jpg)

Después, es necesario que [descargues e instales git](http://git-scm.com/downloads) 
en el ordenador donde vayas a trabajar. En windows es tan sencillo como instalar cualquier
otro programa, así que no hay excusa para parar aquí.

Para configurar git y poder usarlo con github, debemos configurarlo. Para ayudarnos, los 
chicos de github se han currado una aplicación, 
[Github for Windows](https://help.github.com/articles/set-up-git). También se puede 
[configurar github en linux](https://help.github.com/articles/set-up-git#platform-linux).

## Obtener el código fuente

Para comenzar a colaborar, necesitas un repositorio donde esté almacenado el código fuente
sobre el cual vais a trabajar. Dos formas muy comunes de crear un repositorio en tu
cuenta de github son:

1. [Crear un repositorio desde cero](https://help.github.com/articles/create-a-repo).
2. [Copiar el repositorio de otra persona (fork)](https://help.github.com/articles/fork-a-repo).

Con tu repositorio en github, ya puedes *descargarlo* a tu máquina de trabajo. En realidad
lo que vas a hacer es una copia entera y completamente funcional del repositorio en github.

```
	git clone https://github.com/username/Spoon-Knife.git
```
Esto creará un directorio llamado `Spoon-Knife` donde se encuentra el repositorio completo.

## Modificar ficheros y subir los cambios

Ya podemos realizar los cambios que queramos al código fuente. 

Para subir estos cambios al repositorio de github, debemos seguir varios pasos:

1. Añadir los fichero nuevos al área temporal de git llamada `stage` para poder hacer `commit`
al repositorio (existen más opciones para este comando, pero el más básico es éste):

```
	git add . 
```

2. Hacer `commit` de esos cambios. De esta forma, nuestro repositorio ya contendrá los cambios, 
sólo hará falta incorporarlos al repositorio de github (repositorio remoto):

```
	git commit -m "Mensaje del commit"
```

3. Subir los cambios del repositorio local al repositorio remoto (github). El comando más básico
para ello es el siguiente:

```
	git push
```

Si vamos a nuestro repositorio en github veremos cómo aparecen los commits que hicimos en nuestro
repositorio local. BIEN!

## Descargar cambios del repositorio de github

Con el siguiente comando (esta es su sintaxis más sencilla) podrás incorporar los cambios que haya
en el repositorio remoto de github a tu repositorio local:

```
	git pull
```

Esta es su sintaxis más sencilla. Para avanzar en este aspecto, tendría que hablar de 
[remotes](http://gitref.org/remotes/), pero es un concepto bastante extenso y quedaría un 
post muy largo.

## Compartir nuestros cambios con los compañeros

De acuerdo, ya tenemos nuestros cambios en nuestro repositorio local y los hemos subido a nuestro
repositorio remoto en github. Existe una forma muy sencilla en github de informar a nuestros compañeros
de que hemos hecho cambios, los llamados 
[Pull Request](https://help.github.com/articles/using-pull-requests).

![Pull Request]({{ site.baseurl }}/assets/images/2013/github-pull-request.jpg)

Mediante un Pull Request estás indicando a un compañero que le quieres pasar unos cambios que
tú has hecho. Ahora tu compañero deberá decidir si acepta los cambios y él incorporará esos 
cambios a su repositorio remoto
