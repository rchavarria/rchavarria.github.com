---
layout: post
title: "Charla técnica: Follow my leader"
date: 2015-10-04 15:21
author: Rubén Chavarría
comments: true
categories: 
- Vim
- technical talks
- learning
published: true
footer: false
sidebar: true
---

Estas notas podrían encajar perfectamente en el post que voy actualizando
regularmente [Aprendiendo Vim], pero creo que esta la charla de Drew Neail se
desmarca ya un poco del proceso de aprendizaje. En esta charla no se busca
enseñar nuevos comandos de Vim, si no que se trata más de un tema cultural
acerca del editor. Drew trata de animar a la gente a que busque nuevas
combinaciones de teclas que se conviertan en nuevos comandos y de esta forma
hacer Vim más potente todavía.

<!-- more -->

## Notas tomadas de la charla [Follow my leader]

<iframe src="https://player.vimeo.com/video/85343734"
        width="500"
        height="281"
        frameborder="0"
        webkitallowfullscreen mozallowfullscreen allowfullscreen>
</iframe>

*[Follow my leader], por [Drew Neil], en un encuentro del grupo local
[Vim London]*

- `let mapleader = ","` para mapear `,` como tecla `<leader>` en Vim. Otra
tecla muy común para utilizarla como `<leader>` es la barra espaciadora.
- `nnoremap <leader><space> :noh<cr>` : remapea la secuencia de teclas
`<leader><space>` para que se ejecute el comando `:nohlsearch`, que desactiva
el resaltado de términos de búsqueda.
- La tecla `<leader>` te permite crear mapeos personalizados, es donde los
usuarios pueden crear sus mapeos sin interferir con Vim
- En lugar de usar `leader`, algunos plugins, como los que escribe [Tim Pope]
siguen otro patrón. hay teclas que son *operadores*, por ejemplo la **d**
para borrar, o la **y** para copiar. a estos operadores le puede seguir el
mismo operador o una movimiento. Teclas que producen un movimiento son **j**
para ir hacia abajo, **$** para ir al final de la línea, ... Pero, qué pasa si
despues de un operador pulsamos una tecla de *no movimiento*? No pasa nada. Y
ahí están las combinaciones de teclas dsiponibles para tus plugins.
- En la imagen de la [chuleta de Vim], los naranjas son operadores, los
verdes movimientos y los amarillos son comandos.

{% img center /images/2015/tiny-vi-vim-cheat-sheet.gif %}

- El plugin [unimpaired.vim] añade mapeos como `con` para habilitar/deshabilitar los
nuḿeros de línea, o `cos` para habilitar/deshabilitar el chequeo ortográfico.
Son `c` + `o` + otras teclas
- También hay disponibles combinaciones como operador + operador : `d` + `c`
- Los *text objects* (`i` y `a`) también tienen vacantes.
- Los *namespaced mappings* también tienen vacantes. Por ejemplo, `g` es como
un prefijo para muchos mapeos. `z` es otro, y `[` y `]` son más.
- `:help g` te muestra todos los mapeos que siguen a `g`. Te puede servir para
ver huecos donde poner tus mapeos
- Comando inútiles, hay algunos comandos que no usa nadie. Sobreescríbelos. Por
ejemplo, `g` + `s`.
- Sobreescribir, sobrecargar comandos que ya existen, vamos, ampliar los
existentes.

## Conclusiones

Como puedes ver, el editor Vim es todo un mundo de posibilidades. Hay veces que 
abruma, pero hay tanta gente apasionada por él que está claro que algo debe de
tener. Esta charla es una muestra de las posibilidades de personalización que
esta herramienta ofrece. Drew nos abre las puertas a un mundo nuevo de posibles
comandos.

Si te gusta Vim, y no conoces el plugin [unimpaired.vim], échale un vistazo. Sin
duda es uno de los imprescindibles, como tantos otros de Tim Pope.

[Aprendiendo Vim]: /blog/2014/10/11/aprendiendo-vim/
[Follow my leader]: https://vimeo.com/85343734
[Drew Neil]: http://drewneil.com/
[Vim London]: https://vimeo.com/vimlondon
[chuleta de Vim]: http://www.viemu.com/vi-vim-cheat-sheet.gif
[Tim Pope]: http://tpo.pe/
[unimpaired.vim]: https://github.com/tpope/vim-unimpaired

