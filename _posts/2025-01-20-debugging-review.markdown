---
layout: post
title: "Artículo de opinión sobre el libro Debugging"
date: 2025-01-20 17:00
author: Ruben Chavarria
categories:
- Libros
- Articulos
- Programacion
---

A través de Hacker News, me llega este artículo, una revisión
del libro [Debugging: 9 rules](https://dwheeler.com/essays/debugging-agans.html)

Ya me lo he apuntado en mi [lista de lecturas]({{ site.baseurl | append:'/readings' }})
porque tiene una muy buena pinta

<!-- more -->

Como resumen, ahí van las 9 reglas del libro, traducidas literalmente
del artículo, no hay nada mío en ellas:

1. **Entiende el sistema**: Lee el manual, lee todo en profundidad, 
conoce los fundamentos, conoce la hoja de ruta, entiende tus herramientas 
y busca los detalles
2. **Haz que falle**: Hazlo de nuevo, empieza por el principio, estimula el fallo,
no simules el fallo, encuentra la condición no controlada que lo hace
intermitente, grábalo todo y encuentra la firma de los fallos intermitentes,
no confíes demasiado en las estadísticas, sabe que «eso» puede pasar, 
y nunca tires una herramienta de depuración
3. **Deja de pensar y mira** (obtén datos primero, no hagas reparaciones complicadas
basándote en suposiciones): mira el fallo, fíjate en los detalles, incorpora 
instrumentación, no tengas miedo profundizar, 
ten cuidado con Heisenberg e intenta adivinar solo para centrar la búsqueda
4. **Divide y vencerás**: acota la búsqueda con aproximaciones sucesivas, 
obtén el rango, determina en qué lado del fallo te encuentras, utiliza patrones
de prueba fáciles de detectar, empieza por lo malo, arregla los fallos que 
conozcas y arregla primero el ruido.
5. **Cambia una cosa cada vez**: aísla el factor clave, entiende qué falla antes 
de arreglarlo, cambia una prueba cada vez, compárala con una buena y determina
qué ha cambiado desde la última vez que funcionó
6. **Lleva un registro de auditoría**: anota lo que hiciste, en qué orden y qué
ocurrió como resultado, comprende que cualquier detalle podría ser el importante,
correlaciona los acontecimientos, comprende que los registros de auditoría 
para el diseño también son buenos para las pruebas, ¡y anótalo!
7. **Comprueba el enchufe**: cuestiona tus suposiciones, empieza por el principio 
y prueba la herramienta
8. **Obtén una nueva visión**: pide ideas nuevas (explicar el problema a un patito 
de goma puede ser útil), recurre a expertos, escucha la voz de la experiencia,
recuerda que hay ayuda a tu alrededor, no seas orgulloso/a, informa de los
síntomas (no de las teorías) y comprende que no tienes por qué estar seguro al 100%
9. **Si no lo has arreglado, no está arreglado**: comprueba que realmente está solucionado,
comprueba que realmente es tu solución la que lo ha solucionado, reconoce que
nunca desaparece por sí solo, soluciona la causa y soluciona el proceso 
