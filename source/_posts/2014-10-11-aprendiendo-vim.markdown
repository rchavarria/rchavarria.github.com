---
layout: post
title: "Aprendiendo Vim"
date: 2014-10-11 01:31
author: Rubén Chavarría
comments: true
categories: 
- Vim
- learning
published: true
footer: false
sidebar: true
---

Hubo un momento en mi carrera profesional en la que un compañero me dió a conocer
*Vim*, el editor de código. Me pareció una herramienta arcaica, básica. Línea
de comandos, nada de modo gráfico. ¿Pero dónde estaba? ¿En los años 80?. Pero la
pasión con la que hablaba del editor mi picaba la curiosidad.

Luego, en años venideros, he visto y usado muchos editores de texto, de código
e incluso IDEs. Nunca me había atrevido a usar Vim, pero de vez en cuando
escuchaba (de la forma que se escucha en internet: twitter, blogs, ...) algunas
campanadas de que Vim era un súper editor.

Pero nunca me decidía a darle una oportunidad, hasta...

<!-- more -->

Hasta que cayó un post de [Pablo Bernardo] en mi lector RSS:
[Asi que quieres aprender a usar Vim].

[Pablo Bernardo]: http://elkarmadelteclado.com
[Asi que quieres aprender a usar Vim]: http://elkarmadelteclado.com/asi-que-quieres-aprender-usar-vim/

En este post, Pablo detalla toda una serie de recursos disponibles en *la nube*
y no sé porqué, pero me tocó la fibra sensible. Y decidí empezar por uno de los
videos.

El video en cuestión, es un hangout de LinuxIO, de [Desarrollo Web], y que se
titula "[El mítico editor Vim]". Este video fue el detonante de que decidiera
darle una oportunidad a Vim, una oportunidad seria. Así que decidí comenzar a
aprenderlo.

[Desarrollo Web]: http://www.desarrolloweb.com
[El mítico editor Vim]: http://youtu.be/cpL32a_GP3k

La idea es que este post no se acabe aquí, si no que vaya creciendo con el
tiempo, que vaya actualizandolo según voy consumiendo los recursos que indica
Pablo, y los que me encuentre por el camino. Para cada uno de ellos me gustaría
ir describiendo qué es lo que he aprendido de él.

De esta forma, según vaya pasando el tiempo, aquí tendré el camino recorrido,
y así otros podrán saber cómo lo recorrí para aprender Vim.

<!--
LinuxIO, con @ktzar, que anima bastante https://www.youtube.com/watch?feature=player_embedded&v=cpL32a_GP3k

Segunda parte del LinuxIO: https://www.youtube.com/watch?feature=player_embedded&v=XvCD78eA46E

Un semi-dios del vim, Drew Neil : https://vimeo.com/53144573

Pagina de Drew Neil : http://drewneil.com/
Con enlaces a vimcasts, peer-to-peer.io, ...

Libros en open libra (no leidos) http://www.etnassoft.com/biblioteca/?search_term=VIM&books_category=libros_programacion&books_criteria=post_date_DESC&lang=all&since=all

Videos de Derek Wyatt : http://derekwyatt.org/vim/tutorials/

-->

## El mítico editor Vim, #linuxIO

[Miguel Luis González] y [Pablo] nos presentan [El mítico editor Vim]. Miguel pone tanta pasión,
tanto conocimiento, que impresiona. Este es el video que me convenció. Y
éste es un resumen de lo que aprendí de él (y estoy poniendo en práctica escribiendo
este post :D ).

[Miguel Luis González]: https://twitter.com/ktzar
[Pablo]: https://twitter.com/voylinux

- Movimientos básicos: `h`, `j`, `k`, `l`. Nada de usar las flechas, ¡Cobarde!
- `i` para **i**nsertar
- `a` para **a**ñadir. Inserta, pero después de la posición del cursor
- `:o <fichero>` para abrir (**o**pen) un fichero
- `:q` para salir del Vim. `:q!` para salir ignorando los cambios
- `:w` para guardar (**w**rite)
- `u` para deshacer (**u**ndo)
- `CTRL + r` para rehacer
- `w` para mover el cursor a la siguiente palabra (**w**ord)
- `b` para mover el cursor a la palabra anterior (**b**efore)
- `e` para mover el cursor al final (**e**nd) de la siguiente palabra
- `x` para borrar un carácter
- `p` para **p**egar. `P` para hacerlo antes del cursor
- `r` para reemplazar un carácter
- `f<carácter>` para encontrar (**f**ind) el siguiente carácter en la línea
- `0` mover el cursor al inicio de la línea. `$` para ir al final
- `d` borrar (**d**elete). `dw` borra palabra. `dd` borra línea
- `c` para **c**ambiar. Por ejemplo, `cw` cambia una palabra. `cc` cambia una linea
- `y` para copiar (**y**ank). `yw` copia una palabra. `yy` una línea. `yf)` copia
hasta que encuentra el caracter `)` inclusive.
- `t<carácter>` para mover hasta (un**t**ill). `yt)` para copiar hasta el carácter
`)` sin copiar el carácter.
- `%` para mover el cursor al carácter complementario. Por ejemplo, si estamos en
un carácter `(`, nos mueve hasta el siguiente `)`. De `[` al `]`. ¿Lo pillas?

<!--
## LinuxIO, Vim avanzado

Mas de @ktzar y @voylinux.

¿Qué aprendí?

- Invocar línea de comandos desde Vim. Pero le veo una pega, que todavía no sé cómo solucionar. No puedo cambiar el directorio de trabajo, por lo que si edito en ~/documents/js y quiero ejecutar un comando sobre ese directorio, no puedo.
- Plugin [Nerd Tree]
- Donde está la configuración de Vim (~/.vimrc)

## Derek Wyatt, movimientos basicos 1

## Derek Wyatt, movimientos basicos 2

## Derek Wyatt, movimientos basicos 3
-->

