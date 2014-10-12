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

## (12-10-2014) Vim sobre Linux, comandos avanzados y plugins 

Miguel y Pablo siguen hablando de Vim, de [comandos avanzados y plugins], temas más
avanzados que en el anterior vídeo, pero con el mismo tono alegre y pasión.
Esto es lo que aprendí en él:

[comandos avanzados y plugins]: http://youtu.be/XvCD78eA46E 

- `s` para sustituir un carácter. Borra el carácter donde está el cursor y entra
en modo edición.
- `C` para cambiar una línea entera.
- Números como modificadores de comandos. Por ejemplo, `5dd` borra 5 líneas. `3yy`
copia 3 líneas.
- `/<texto>` para buscar la cadena de texto hacia adelante
- `n` para moverse a la siguiente (**n**ext) ocurrencia de la búsqueda. `N` para
moverse a la anterior.
- `?<texto>` para buscar la cadena de texto pero hacia atrás
- `*` entra en modo búsqueda, usando la palabra donde estamos como texto de búsqueda
- *Movimientos interiores*. `i` expande el cursor o la selección en el **i**nterior
de un texto encerrado entre dos comillas, o dos paréntesis, o dos llaves.
Por ejemplo, `ci'` **c**ambia el **i**nterior del texto entre comillas. `di(`
borra (**d**elete) el **i**nterior del texto entre paréntesis. `cit` **c**ambia
el **i**nterior del **t**ag HTML.
- `v` entra en modo **v**isual. `V` modo **v**isual línea a línea
- `CTRL + v` entra en modo **v**isual pero selecciona columnas
- `CTRL + p` autocompletado, buscando en palabras anteriores a la actual y en todos
los ficheros abiertos. `CTRL + n` muestra también una lista de posibles palabras
para autocompletar, pero dando preferencia a texto encontrado hacia abajo
- `%s/<texto a buscar>/<texto a reemplazar>/g` busca y reemplaza un texto por otro,
se puede hacer en todo el fichero o dentro de una zona seleccionada con `v`
- `=` indenta un texto. `==` indenta una línea entera
- `<` y `>` aumentan o disminuyen la indentación de la línea
- `gg` mueve el cursor al inicio del fichero. `G` lo mueve al final del fichero
- `:!<comando unix>` ejecuta un comando unix. `%` se reemplaza por la ruta del
fichero actual. También puede actuar sobre regiones de selección visuales.
`:'<, '>!sort` ordena la selección visual
- `q<tecla>` comienza la grabación de una macro, almacenándola en `<tecla>`. Volver
a pulsar `q` para parar la grabación. 
- `@<tecla>` ejecuta la macro almacenada en `<tecla>`
- `@@` ejecuta la última macro
- `:split`, `:vsplit` para abrir varios ficheros y verlos simultáneamente
- `:buffer <número>` para abrir un buffer o nuevo fichero. Por ahora los buffers
es un tema algo complicado. Más adelante aprenderé más sobre ellos.

Plugin [NERDTree](http://vim.sourceforge.net/scripts/script.php?script_id=1658).
Con `CTRL + w` se entra en un modo para poder moverse por las
ventanas (**w**indows). Se pueden utilizar las teclas de movimiento `h`, `j`, `k`, `l`
para moverse por los ficheros que muestra el plugin en forma de árbol.

Se puede utiliar Vim como una herramienta para comparar ficheros. El comando unix
`vimdiff` abre Vim con dos ficheros para compararlos.

Toda la configuración de Vim se guarda en el directorio `~/.vim`. Los plugins se
guardan en `~/.vim/plugin` y los ficheros de ayuda en `~/.vim/doc`. Configuraciones
de teclas, colores, indentación y otras se guardan en el fichero `~/.vimrc`.

Plugin [Command-T](https://wincent.com/products/command-t). Para abrir ficheros con
las teclas `CTRL + t`. Parecido a la misma funcionalidad de TextMate o Sublime. Al
parecer necesita Ruby, así que la instalación quizá no sea muy sencilla.

## (12-10-2014) Derek Wyatt: Basic movements II

El primer video de Derek decidí saltármelo, ya que todos los comandos estarían 
cubiertos con los videos de #LinuxIO. En el de [Movimientos básicos II](http://vimeo.com/6185584)
aprendí lo siguiente:

- `H` mueve el cursor a la cabecera (**h**ead) del texto que se muestra en pantalla
- `M` mueve el cursor a la parte **m**edia del texto en pantalla
- `L` mueve el cursor a la última (**l**ast) línea del texto en pantalla
- `<número>G` nos lleva a la línea número `<número>`
- `#` busca la palabra sobre la que buscamos, pero hacia atrás. Es como el comando
que ya vi anteriormente `*`
- `g*` busca el texto, como `*`, pero no tiene porqué ser la palabra completa

## (12-10-2014) Derek Wyatt: Basic movements III

En el video de [Movimientos básicos III](http://vimeo.com/6216655) ya no podían quedar
muchos más movimientos que aprender, y la verdad es que los que aquí aparecen son ya
movimientos un poco más extraños, aunque no por eso dejan de ser útiles.

- `:help motion.txt` para ver la ayuda sobre movimientos, para que no se olvide
ninguno
- `]]` mueve el cursor hasta el siguiente carácter `{` que exista en la columna 0.
Ideal para movernos por ficheros de código. Existen otras combinaciones, como 
`[[`, `[]` y `][`, pero actuando sólo sobre la columna 0, no sé si les voy a sacar
mucho provecho.

El plugin [matchit](http://www.vim.org/scripts/script.php?script_id=39) amplía la
funcionalidad del comando `%` (que movía el cursor hasta el siguiente carácter
complementario: de `(` a `)`, de `[` a `]`, ...).

`:help marks` para conocer acerca de marcadores. No los suelo utilizar en mi día
a día, pero no está de más saber que existen.

- `m<tecla>` define un marcador en `<tecla>`
- `'<tecla>` nos mueve al marcador definido en `<tecla>`
- `''` nos lleva al último lugar donde editamos, ya que Vim almacena en `'` dicha
posición de forma automática

## (13-10-2014) Derek Wyatt: basic editing I

No es que aprendiera mucho en el video de [Edición básica](http://vimeo.com/6329762) de 
Derek, pero la mayoría de comandos ya estaban cubiertos con los videos de #LinuxIO.

- `x` borra el carácter donde esta el cursor. `X` borra hacia atrás
- `r` **r**eemplaza un carácter. `R` **r**eemplaza varios carácteres, hasta que pulsemos `ESC`.
`5rx` reemplaza 5 caracteres por una `x`.

El comando `:set cpoptions+=$` configura una funcionalidad adicional para el 
comando `c` (**c**ambiar). Lo que hace es que aparezca el carácter `$` al 
final del texto que se va a cambiar.

## (13-10-2104) Derek Wyatt: basic editing II

No hay gran cosa que destacar en el video de
[Edición básica II](http://vimeo.com/6332848).

- `F<carácter>` encontrar (**f**ind) un carácter hacia atrás
- `J` une (**j**oin) una línea con la inmediatamente inferior. `gj` une dos líneas
sin dejar ningún espacio en blanco. 
- `gv` selecciona el último bloque visual 

## (13-10-2014) Derek Wyatt: working with many files I

En el episodio de [Múltiples ficheros I](https://vimeo.com/6306508) aprendí un
manejo básico de buffers, es decir, manejar varios ficheros a la vez.

- `:e <fichero>` abre un buffer con ese <fichero>
- `:ls` lista todos los buffers abiertos
- `:buffer <número>` cambia al buffer número `<número>`. `:b <nombre>` cambia al
buffer del fichero con el nombre `<nombre>`. `b#` cambia al buffer anterior.
- `:bdelete` o `bd` cierra el buffer abierto en ese momento
- `:%bd` cierra todos los buffers (`%` significa *todo el rango*)

## (13-10-2014) Derek Wyatt: working with many files II

El episodio de [Múltiples ficheros II](https://vimeo.com/6307101) sigue enseñándome
a manejar varios buffers o ficheros a la vez.

- `:wn` (**w**rite and move **n**ext), escribe el buffer actual y se mueve al
siguiente
- `:n` mueve al siguiente (**n**ext) buffer
- `:bufdo <comando>` ejecuta el comando en todos y cada uno de los buffers
abiertos
- `:wall` escribe todos (**all**) los buffers
- `:bfirst` se mueve al primer buffer. `:bn` se mueve al siguiente. `:bp` se
mueve al anterior (**p**revious)

Todos estos comandos son potentes si se usa **una sola sesión de Vim**, y
son inútiles si tienes abiertos N Vims con N ficheros. Así que recuerda:
una sola sesión de Vim.

## (13-10-2014) Derek Wyatt: working with many files III

En el [último episodio sobre múltiples ficheros](https://vimeo.com/6342264)
hay más y más comandos que aprender, a cual más útil.

- `CTRL-w o` te deja con sólo una ventana abierta
- `:split <fichero>`, `:sp <fichero>` divide la pantalla y abre una ventana debajo
de otra con el nuevo fichero
- `CTRL-w x` intercambia (e**x**change) dos ventanas
- `CTRL-w v` divide la pantalla en vertical, mostrando dos ventanas con el mismo
buffer. También se puede hacer con `:vsplit` o `:vsp`
- `CTRL-w` seguido de `h`, `j`, `k` o `l` te permite moverte de ventana en ventana
igual que si lo estuvieras haciendo dentro de un fichero
- `CTRL-w` seguido de `H`, `J`, `K` o `L` mueve la ventana a la derecha, abajo,
arriba o a la derecha
- `CTRL-w p` mueve el cursor a la última ventana visitada
- `CTRL-w c` **c**ierra la ventana
- `CRTL-w` mueve el cursor a la siguiente ventana, de una en una, una especie de
`CTRL-TAB` o así

- `CTRL-w c` **c**ierra la ventana
- `CRTL-w` mueve el cursor a la siguiente ventana, de una en una, una especie de
`CTRL-TAB` o así

<!--

## (14-10-2014) Derek Wyatt: how to use the help system

Para aprender acerca de [cómo usar la ayuda](http://vimeo.com/7035132) este
video es lo mejor, aquí va un resumen:

- 

-->

