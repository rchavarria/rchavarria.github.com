---
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

## Recursos para aprender

- [Primera parte del LinuxIO](https://www.youtube.com/watch?feature=player_embedded&v=cpL32a_GP3k): con @ktzar que anima bastante
- [Segunda parte del LinuxIO](https://www.youtube.com/watch?feature=player_embedded&v=XvCD78eA46E)
- [Charla de Drew Neal](https://vimeo.com/53144573), un semidios de Vim. Página de Drew [http://drewneil.com/](http://drewneil.com/), con enlaces a VimCasts, peer-to-peer.io,...
- [Libros de Vim](http://www.etnassoft.com/biblioteca/?search_term=VIM&books_category=libros_programacion&books_criteria=post_date_DESC&lang=all&since=all) en OpenLibra
- [Videos de Derek Wyatt](http://derekwyatt.org/vim/tutorials/)
- [Vim golf](http://vimgolf.com/)
- [Vim Kata meetup](https://github.com/christoomey/vim-kata-meetup), de Chris Toomey
- [Vim galore](https://github.com/mhinz/vim-galore)
- [Vim GIFs](https://vimgifs.com/): un recurso muy visual, con *videos* diarios sobre comandos muy específicos del editor. Ideal para consumir pequeñas píldoras cada día. También en Twitter [@vimgifs](https://twitter.com/vimgifs)
- [Vim configuration from scratch](http://marcgg.com/blog/2016/03/01/vimrc-example/): una completa y básica guía de cómo deberías tener configurada tu configuración de Vim, teniéndola bajo un control de versiones, cada plugin en un submódulo git,...

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

## (14-10-2014) Derek Wyatt: how to use the help system

Para aprender acerca de [cómo usar la ayuda](http://vimeo.com/7035132) este
video es lo mejor, aquí va un resumen:

- `:help` o `:h` abre una ventana como si fuera un buffer donde muestra la ayuda
- `CTRL+]` para seguir un hiperenlace de la ayuda (no se si funcionara con 
teclado español). `CTRL+t` para volver hacia atrás
- `:help <tag>` abre la ayuda de una etiqueta. Las etiquetas tienen la forma
de `*:<command>*` en la ayuda.
- `:help <function>()` abre la ayuda de una función
- the command `wildmenu` (o `wmnu`) habilita el autocompletado de comandos en
con `TAB`. Para activarla, escribir `:set wildmenu`. Para desactivarla
`:set nowildmenu`
- `:helpgrep` (`:helpg`) busca un patrón en los ficheros de ayuda. Con el
filtro `[@xx]` busca sólo para el lenguaje `xx`. Para movernos por los resultados
se puede hacer con `:cn` (siguiente o **n**ext) o con `:cwin` nos abre una
ventana llamada *quickfix* (`:h quickfix` para saber más)


## (23-10-2014) Derek Wyatt: Vim runtime y el fichero .vimrc

Sigo aprendiendo Vim con este tío, esta vez sobre el 
[fichero de configuración .vimrc y el runtime](http://derekwyatt.org/vim/tutorials/intermediate/#vimrc):

- El fichero `vimrc` se usa para configurar Vim cuando arranca
- En Linux, el fichero `vimrc` se encuentra en `~/.vimrc`
- Puedes escribir los mismos comandos que en el modo comando, cuando empieza por `:`
- Echar un vistazo a MiniBufExplorer plugin
- `:h vimrc` para leer la ayuda
- `nnoremap` es un comando interesante para remapear ciertos comandos
- `:h 'runtimepath'` muestra la ayuda sobre vim runtime path
- `~/.vim/` es el runtime path por defecto en Linux. Ahí es donde irán instalados
los ficheros de ayuda, los plugins, los colores de syntaxis, ...
- `~/.vim/doc` es donde se guarda la ayuda
- `~/.vim/colors` es donde se guardan los esquemas de colores
- `~/.vim/plugin` es donde *viven* los plugins

## (24-10-2014) Derek Wyatt: Vim modes introduction

Los modos es la característica que diferencia a Vim (sobre todo de emacs, su eterno
enemigo), y ya iba siendo hora de apreder sobre ellos. Los modos de Vim son:
normal, visual, inserción, comando y ¿¡ejecución!?, así que aquí va una
[introducción a los modos de Vim](http://derekwyatt.org/vim/tutorials/intermediate/#modes-intro):

- modo *Normal*: donde puedes introducir los comandos del editor
- modo *Visual*: como el modo normal, pero según te mueves por el fichero, el texto
se va resaltando, como si fuera una selección visual
- modo *Inserción*: es el modo donde se introduce el texto
- modo *Línea de comandos*: donde puedes introducir comandos en una línea abajo
del todo de la ventana de Vim. Los comandos comienzan con `:`, `/`, `?` o `!`
- Y hay otros modos menos usados, que más que modos distintos son como una
mezcla de varios de los básicos, como el modo *Inserción Normal*, que, estando
en el modo de inserción, te permite ejecutar un comando (uno sólo) y luego
vuelve a entrar en el modo de inserción.

## (28-10-2014) Derek Wyatt: Insert mode

En este video Derek profundiza en uno de los modos importantes de Vim, el
[modo de inserción](https://vimeo.com/7133419), en el cual podemos usar
autocompletado, indentar líneas y muchas cosas más.

- `:help i_CTRL-A` muestra la ayuda para la combinación de teclas `CTRL a` pero
exclusivamente para el modo de inserción, de ahí el `i_`
- `expandtab` es una opción que indica el número de espacios a insertar cuando
se presiona la tecla `TAB`
- `CTRL w` borra la palabra anterior (si estamos en modo de inserción)
- `CTRL t` incrementa en uno la indentación
- `CTRL d` decrementa en uno la indentación
- `:help ins-special-special` muestra la ayuda de comandos en el modo inserción,
como por ejemplo `CTRL g j` para mover el cursor una línea abajo.
- `CTRL m`, `CTRL p` busca palabras para autocompletar buscando hacia abajo o
hacia arriba
- `CTRL x` + `CTRL l` autocompleta líneas enteras, es decir, en lugar de buscar
palabrejas, busca líneas completas.
- `CTRL x` + `CTRL f` autocompleta rutas de ficheros

## (02-11-2014) Derek Wyatt: One Vim... just one

Es cortito video acerca de [mantener una y solo una sesión de Vim](http://vimeo.com/4446112)
se enfoca en solamente un comando de la shell:

    gvim --remote-silent

Este sencillo comando nos permite abrir varios ficheros en una única sesión
gráfica de vim.

Tal y como dicen los comentarios del vídeo, este comando solamente funciona por
defecto en la interfaz gráfica de Vim, no en la versión de Vim que se ejecuta
en la línea de comandos.

## (02-11-2014) Derek Wyatt: Destruction is good

En este video Derek muestra cómo utilizar
[comandos destructivos para editar](http://vimeo.com/6110008)
el contenido que queremos.

Comandos utilizados:

- `:v/<some pattern>/<some command>`: es el comando `:vglobal` (usar `:help :vglobal`
para saber más). Este comando realiza acciones sobre líneas que NO cumplen el patrón
especificado.
- `:help :substitute` muestra ayuda del comando utilizado para sustituir unas cadenas
por otras.
- Expresiones regulares, que son ya un problema en sí mismas y que darían para
mucho tiempo de aprendizaje.

## (24-11-2014) Derek Wyatt: Using a Vim macro to edit many files

Y después de un tiempo sin ver nada nuevo de Vim, hoy toca ver cómo se puede
[utilizar una macro para editar varios ficheros](http://vimeo.com/4456458), del cual,
se pueden sacar los siguientes macros y consejos:

- `q + a` para comenzar a grabar una macro en la posición `a` 
- `@ + a` para ejecutar la macro grabada en la posición `a`
- `@ + @` para ejecutar la última macro
- `5 + @ + a` para ejecutar la macro en `a` 5 veces
- `:wn` guardar todos los cambios y moverse al siguiente buffer
- `:prev` moverse al buffer anterior
- `" + a + p` imprime la macro guardada en la posición `a`

## (08-01-2015) Derek Wyatt: Vim macros and global commands

Sigo aprendiendo cosas sobre Vim, esta vez sigo con 
[macros en Vim y comandos globales](https://vimeo.com/4448635). Estos son los
comandos y nuevos consejos que aprendí:

- `CTRL + A` incrementa en uno el primer número que encuentra en la línea
- `20 CTRL + A` incrementa en 20 el primer número de la línea
- Grabar y ejecutar macros, visto en el anterior
- `:g/sometext/normal 20^A` es un comando global (en modo :normal, lo que sea eso
que signifique), que busca la cadena `sometext` (ya he visto antes cómo buscar
cadenas de texto) y ejecuta el comando `20 CTRL + A`. Para ello, para poder
escribir `CTRL + A` como comando, hay que pulsar `CTRL + V` para que la 
siguiente pulsación la tome de forma literal, y luego pulsar `CTRL + A`
- `CTRL + V` hace que Vim tome la siguiente pulsación de forma literal, muy útil
cuando se escriben comandos globales, por ejemplo.

## (08-01-2015) Derek Wyatt: Vim expression register

Una vez acabados los vídeos de nivel intermedio, toca comenzar con los de
nivel avanzado. Comienzo con el [registro de expresiones](http://vimeo.com/4446843). ¿Qué es?
¿Para qué sirve? En el vídeo lo descubro:

- ¿Qué es? Es un registro, un lugar donde almacenar *cosas*. ¿Y qué cosas
son esas? Pues son comandos.
- ¿Para qué sirve? Lo utilizan los programadores de plugins para extender
Vim y para integrarlo con herramientas de terceros.
- `:imap <c-j>d <c-r>=system('echo foo')<cr>` mapea (en modo **i**nserción)
la combinación de teclas `CTRL + J, D` para que ejecute el comando de 
sistema `echo foo` e inserte el resultado en el archivo que estamos
editando. `<c-r>` significa `CTRL + R`, que accede al *registro de expresiones*
del que estamos hablando.

## (18-01-2015) Derek Wyatt: Vim autocomands

Siguiendo con vídeos de nivel avanzado, esta vez toca *auto comandos*. Parece
una funcionalidad super útil de Vim. Es una funcionalidad donde puedes configurar
Vim para que realice los comandos que quieras cuando ocurra algún evento: por
ejemplo, cuando se guarda un fichero en disco, o cuando se mueva el cursor.
El vídeo está disponible en [Autocomandos](http://vimeo.com/4454614),
y es muy cortito, que no te de pereza.

- `:help :autocmd`

### (18-01-2015) Derek Wyatt: Find command and the path

El vídeo anterior era realmente corto, y solamente saqué en claro un comando
para Vim, `:autocmd`, pero para su uso es necesario de tener funciones u
otros comandos para que realmente haga algo. 

Así pues, el siguiente es [Find command and the Path](http://vimeo.com/6154082)
para aprender a buscar ficheros y cargarlos para su edición.

- `:set path=<directorio>`: establece la variable `path` en Vim, para búsqueda
de ficheros por ejemplo.
- `:find <filename>`: busca por un fichero y lo abre para su edición
- `:pwd`: muestra el directorio de trabajo actual

### (Marzo 2015) Comando `set statusline`

Esta vez no tengo nada de ningún video, pero es igualmente interesante. Mediante
el comando `set statusline` se puede configurar la apariencia de la *barra de
estado* de Vim. Existen muchos símbolos (por llamarlos de alguna manera) que a
modo de función `printf` pueden ser sustituidos por diversos campos dentro del
editor: nombre del fichero, número de línea, codificación del fichero,...

A partir de [esta pregunta en Stack Overflow](http://stackoverflow.com/questions/21069164/osx-vim-set-laststatus-2-shows-only-the-filename-but-i-want-to-see-everythin)
encontré el fichero de configuración de [sk1418](https://github.com/sk1418/myConf/blob/master/common/.vimrc#L506)
en el cual me basé para crearme mi propia configuarción de la barra de estado:

    set laststatus =2 " always show status bar
    set statusline=%<%f%h%m%r%=%b\ 0x%B\ \ %l,%c%V\ %p\ %P

La cual me muestra:

- Nombre del fichero, con la ruta completa
- Una marca para saber si el fichero está modificado
- Valor decimal del carácter donde está situado el cursor
- Valor hexadecimal del mismo
- Columna o línea del fichero donde está el cursor
- Fila
- Tanto por ciento del fichero donde está el cursor

### (Mayo 2015) [Why, oh why, do those #?@! nutheads use vi?](http://www.viemu.com/a-why-vi-vim.html)

Después de un cierto tiempo, tropecé con éste post, del cual extraje algún que
otro comando que no conocía todavía. Y no solo comandos, sino secuencias de ellos
que me permiten realizar tareas muy comunes en el desarrollo de software.

*Extraer una variable*

```
if (!entry.used && equivalent(entry.key(), qk.key) && (curcontext & entry.contexts)) {
    // do something
}
```

Situar el cursor al principio de `equivalent` y teclear el comando `c%`:

```
if (!entry.used && <cursor will be here> && (curcontext & entry.contexts)) {
    // do something
}
```

Resulta que eso **c**orta el texto `equivalent(entry.key(), qk.key)` y entra en modo
edición. Luego puedo escribir el nombre de la variable, cambiar a modo normal
y pulsar `O` para insertar una línea arriba:

```
<cursor here>
if (!entry.used && equiv && (curcontext & entry.contexts)) {
    // do something
}
```

Luego, puedo declarar la variable, y pegar lo que hay en el portapapeles con `CTRL + R`:

```
bool equiv = equivalent(entry.key(), qk.key);
if (!entry.used && equiv && (curcontext & entry.contexts)) {
    // do something
}
```

- `zt`: Mueve la línea (hace **z**oom) donde está el cursor arriba del todo
(**t**op)
- `zz`: Mueve la línea (hace **z**oom) donde está el cursor al centro de la
pantalla
- `zb`: Mueve la línea (hace **z**oom) donde está el cursor abajo del todo
(**b**ottom)
- `*`: busca hacia adelante la palabra seleccionada
- `#`: busca hacia atrás
- `=aB`: corregir la indentación (`=`) de un (**a**) **Bloque**
- Comando `hlsearch`, por ejemplo: `:set hlsearch`
- `gU`: convierte a mayúsculas todo el texto seleccionado
- `gu`: convierte a minúsculas todo el texto seleccionado

### (Junio 2015) [A casual introduction to Vim on Windows](https://www.youtube.com/watch?v=xJz2Hq-jWxY)

Por casualidad encontré este vídeo de Roy Osherove, donde habla acerca de Vim
(en Windows, aunque el sistema operativo tiene poca influencia para el nivel
que Roy nos cuenta). No aprendí ningún comando nuevo, porque Roy habla de comandos
básicos, para comenzar a usar Vim, pero creo que el vídeo es un recurso esencial
para el aprendizaje de Vim, por lo que lo enlazo aquí.

### (Julio 2015) [Contar palabras](http://vim.wikia.com/wiki/Word_count)

De repente, escribiendo un post para este blog, me pregunté: ¿Será muy largo
el post?, ¿Cuántas palabras habrá?. Tampoco tengo claro cuantas palabras hacen
que un post sea largo, pero bueno, tenía curiosidad por saber cuántas palabras
había en el post.

El problema es que escribí el post en Windows. Si hubiera estado en Linux, las
hubiera contado con `wc -w`. Estaba en Vim, y decidí buscar algún plugin que
contara las palabras por mí. En lugar de eso, encontré un comando:

- `g` + `CTRL g`

### (Julio 2015) [Mastering the Vim language], Chris Toomey

- Priorizar *text objects* frente a movimientos (`iw` frente a `w`), hacen que
los comandos sean más repetibles, ya que seleccionan mejor. El movimiento `w`
sólo selecciona la palabra si el cursor está al inicio de la misma.
- [repeat.vim] es un plugin que que remapea `.` (commando repetir) de tal forma
que los comandos de los plugins sean compatibles con `.`
- `:set relativenumber`, `:set norelativenumber`, para ver el número de líneas
relativas respecto a la que está el cursor

**Algunos plugins**

- [surround plugin]: 
  - `ds"` : borra las comillas dobles de alrededor
  - `cs"'` : cambia las comillas dobles que encierran el texto por comillas simples
  - y unos cuantos más, como `cst<text>` para cambiar tags HTML
- [commentary plugin]: parece mucho más potente que el que proporciona comandos
`gcc` y demás. éste proporciona `cm<motion>`, por ejemplo: `cml` (comenta línea),
`cm4j` (commenta 4 líneas hacia abajo)
- [replace with register plugin]: con el comando `gr<motion>`, por ejemplo,
si tengo copiada una palabra, puedo hacer `griw` para *go replace inner word*
- [sort-motion plugin]: con el comando `gs<motion>` lo que hace es ordenar
líneas alfabéticamente (para imports, requires,...)
- [system-copy plugin]: para copiar al portapapeles del sistema

**Text objects personalizados**

- indentación: `cmii`, `cmni"`
- entero: `cmae` (**c**omment **a**ll **e**ntire, comenta el documento entero)
- línea: `cml` 

[Mastering the Vim language]: https://www.youtube.com/watch?v=wlR5gYd6um0
[repeat.vim]: https://github.com/tpope/vim-repeat
[surround plugin]: https://github.com/tpope/vim-surround
[commentary plugin]: https://github.com/tpope/vim-commentary
[replace with register plugin]: http://www.vim.org/scripts/script.php?script_id=2703
[sort-motion plugin]: https://github.com/christoomey/vim-sort-motion
[system-copy plugin]: https://github.com/christoomey/vim-system-copy

### (Agosto 2015) [Let Vim do the typing](https://www.youtube.com/watch?v=3TX3kV3TICU), by George Brocklehurst

- `"a` + `p`: pega lo que hay en el registro `a`
- En modo inserción, `CTRL + r` + `<letra del registro>`, pega lo copiado en un
registro
- `CTRL + a`, en modo inserción, pega el último texto insertado
- `CTRL + p`, `CTRL + SHIFT + p`, `CTRL + n`, para autocompletar palabras en los
documentos abiertos de Vim
- Con un fichero CTAGS, si escribo el nombre de una clase y presiono `CTRL + }`
(o `CRTL + ]` no lo tengo claro), Vim me lleva a la declaración de esa clase
- Con `CTRL + x` entra en el modo de autocompletado (palabras, líneas, párrafos,...)
- Después de un `CTRL + }`, puedes volver a navegar hacia atrás con `CTRL + o`
- `CTRL + x` seguido de `CTRL + f` entra en el modo autocompletar nombres de
ficheros
- Con `CTRL + x` seguido de `CTRL + p` puedes ir autocompletando palabras de una
frase. Cada vez que pulsas los dos, puedes ir autocompletando una palabra
- Con `CTRL + x` seguido de `CTRL + n` lo mismo pero en el otro sentido
- Con `CTRL + x` seguido de `CTRL + l` se autocompletan líneas. Si sigues con
`CTRL + x` -> `CTRL + l` te va autocompletando siguientes líneas
- Con `CTRL + x` -> `CTRL + o`, qué tal si te puede autocompletar métodos en tu
lenguaje de programación. No necesita plugin
- `:set complete` muestra tu configuración de autocompletado. el valor por
defecto que muestra es: `.,w,b,u,t,i,kspell`. `.` del buffer actual, `w` de
las ventanas abiertas, `b` de los buffers abiertos, `u` de los buffers no
activos, `t` de los ficheros CTAGS, `i` de los includes/requires, `kspell`
en los diccionarios cuando tengas activado el chequeo de ortografía
(`:set spell`)
- [Repositorio de George](https://georgebrock.github.io/talks/vim-completion), por si se necesita algún documento de referencia

### (29-08-2015) Derek Wyatt: Globals, commands and functions

El último vídeo de Derek, de su lista de [vídeos para aprender Vim]. Este vídeo se
titula [Globals, commands and functions], y estas son las notas que tomé mientras
lo estuve viendo:

- `:saveas <path>`: para guardar un fichero con un nuevo nombre
- `:set ft=xml`: establece el tipo de fichero (`ft`) a `xml`
- `=g` (o `=gg`): para indentar todo el fichero
- `:%s/<regexp>/<text>/`: sustituye globalmente en todo el fichero. Dentro de la expresión regular, podemos crear grupos de texto encerrados entre `\(` y `\)`. Estos grupos serán recordados y podrán incluirse en la parte del texto mediante `\1`, `\2`,...
- `:g`: comando **g**lobal. Permite ejecutar comandos (**i**nsertar, borrrar, copiar,...) desde la línea de comandos. Ver `:help :g`
- `:v`: igual que `:g` pero a la inversa. Por ejemplo, `:v/^foo/d`, busca las líneas que empiezan con `foo`, y las que no lo hacen, las borra. Es decir, ejecuta un comando en las líneas que NO cumplen una condición
- `:normal`: te permite ejecutar comandos del modo normal desde la línea de comandos
- `:normal gggqG`: ejecuta los comandos `gg` (ir al inicio del fichero), `gq` (corta las líneas al ancho especificado con `set tw=<width>`), `G` hasta el final del fichero
- `gq`: inserta carácteres de nueva línea para adecuar el ancho de línea al especificado con `:set tw=<width>`
- `:g/^-/s/- //`: es un comando global (`:g`), para aquellas líneas que
  comienzen con `-`. El comando es **s**ustituir (`s`) los carácters `- ` con
`vacío`
- `:%s/\s\{4}//`: sustituye en todo el fichero exactamente 4 espacios en blanco
  (`\s\{4}`) con `vacío`
- `\zs` en medio de una expresión regular de sustitución: hace que la
  sustitución comienze a partir de ahí. Por ejemplo: `:%s/\s\{8}\zs-/#/` hace
que busque 8 espacios en blanco seguidos de un guión, y que sustituya a partir
de los 8 espacios en blanco, que no los toque
- `:history`: muestra un histórico de los últimos comandos de la línea de
  comandos (`:history : -20` muestra sólo los últimos 20)

[vídeos para aprender Vim]: http://derekwyatt.org/vim/tutorials/advanced/
[Globals, commands and functions]: https://vimeo.com/15443936

### (Septiembre 2015) [My first Vim plugin], de Chris Toomey

En la charla [My first Vim plugin] aprenderemos a crear plugins para Vim. No te
asustes, no es para tanto. También aprenderemos a crear funciones que se puedan
llamar desde la línea de comandos de Vim, éste es el inicio de cualquier
plugin.

- `:set spell`: activa la corrección ortográfica
- `]s`: lleva el cursor al primer error ortográfico que encuentre
- `z=`: muestra un menú con las opciones para corregir el error ortográfico
- `1z=`: selecciona (sin abrir el menú) la primera opción de correción 
- `m<letra>`: establece un marcador en la posición donde está el cursor ahora mismo.
- `<backtic><backtic><letra>`: mueve el cursor hasta el marcador que diga `<letra>`
- `:normal! <comando>`: ejecuta tal cual el comando que le escribamos. Por
ejemplo, si escribimos `:normal! mm]s1z=<back-tick>m`, ejecuta lo siguiente:
establece un marcador en `m` (`mm`), va al primer error ortográfico (`]s`),
lo corrige con la primera opción (`1z=`), vuelve el cursor a la posición donde
estábamos (`<back-tick>m`)
- En un fichero de configuración de Vim:

```
nnoremap <leader>sp :normal! mm]s1z=`m<cr>
# no olvidar <cr> al final, es como pulsar <enter>
```

Lo que hace es asignar la sequencia de comandos `<leader>sp` para que ejecute
el comando que hemos estado hablando. Y qué tecla es `<leader>`? Dice que
normalemente es `\`, pero que él la tiene mapeada a `<spacebar>`. Otra gente
la suele tener mapeada a la coma.

Ahora, lo englobamos en una función:

```
function! FixLastSpellingError() {
    normal! mm]s1z=`m
}
nnoremap <leader>sp :call FixLastSpellingError
```

- `{` mueve el cursor al inicio del párrafo, `}` lo mueve al final
- con `kmmjdd{p<back-tick>m` podemos mover una línea arriba del todo del párrafo (al principio
de una lista, por ejemplo): sube una línea, pone un marcador, baja, borra la línea,
se mueve al principio del párrafo, pega y vuelve al marcador. 
- `yypVr=<cr>`: marca una línea como el primer título de Markdown: 
copia la línea, la pega debajo, se mueve debajo, selecciona
visualmente la línea completa, reemplaza todo con `=`.

**Plugins**

- quicklink: para visitar enlaces que tengas en un fichero Markdown
- text-obj-indent: son objectos de texto adicionales, como por ejemplo un nivel 
de indentación
- sort-motion: permite ordenar con comandos de movimiento: palabra, linea, párrafo,...
- tmux_nav y tmux_runner: para manejar sessiones de tmux desde Vim, abriendo
ventanas en Vim y enviando comandos a ellas

[My first Vim plugin]: https://www.youtube.com/watch?v=lwD8G1P52Sk

<!-- 
  ¿Queda algo por aprender por aquí, o simplemente repasar ya?
-->

