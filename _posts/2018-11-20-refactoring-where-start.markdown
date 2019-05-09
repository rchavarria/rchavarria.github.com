---
layout: post
title: "Refactorizar, ¿por dónde empiezo?"
date: 2018-11-20 00:00
author: Ruben Chavarria
categories:
- Artículos
- Refactoring
---

Notas sobre el artículo de [J.B. Rainsberger] titulado
[Refactoring: where do I start?]. Rainsberger es una persona a la que
admiro como profesional, suele expresarse con bastante claridad y 
suele hablar/escribir/comunicar sobre temas que me interesan bastante.

<!-- more -->

*Refactoring* es una habilidad clave a desarrollar, ya que reescribir
las aplicaciones cuesta mucho y se es tolerado bastante menos.

## ¿Qué es el refactoring?

Es mejorar el diseño del código existente.

Se usa la metáfora de *olores de código* para describir problemas en 
la estructura del código, de tal forma que refactorizar consiste en 
identificar olores en el código, decidir cómo eliminar dichos olores 
y luego transformar sistemáticamente el código, en pasos pequeños y 
reversibles, hasta que el olor desaparezca.

## ¿Cómo me convierto en alguien bueno refactorizando?

Debo aprender 3 cosas:

1. Cómo identificar olores en el código
2. Cómo aplicar refactorizaciones
3. Qué refactorizaciones eliminan qué olores

## ¿Por qué necesito refactorizar?

El código se pudre poco a poco. Las refactorizaciones refrescan el
producto. Cuanto más esperes a refactorizar tu código, más esfuerzo
vas a necesitar para mantenerlo en el tiempo.

## ¿Cómo refactorizo código que no conozco?

Los primeros contactos con código que no conozco son aquellos donde
voy aplicando la refactorización más sencilla y menos arriesgada:
renombrado.

Cuando no conozco el impacto de un cambio en el resto del sistema, busco
maneras de crear cambios poco arriesgados que creen un lugar seguro
donde ir trabajando.  Normalmente introduzco interfaces en los límites
del código que quiero cambiar. La extracción de interfaces es uno de
los cambios estructurales más seguros que uno puede hacer en un
repositorio de código.

## ¿Por qué debería refactorizar cuando simplemente puedo usar patrones de diseño?

Una vez que dominas lo básico de las refactorizaciones, comenzarás a desarrollar
habilidades acerca de juzgar cuándo avanzar hacia un patrón o alejarte de él.

## ¿Cómo se que estoy mejorando el diseño?

Me guio por [las 4 reglas de un diseño simple] de Kent Beck:

1. Pasa todos los tests
2. Minimiza duplicación (en todos sus sentidos)
3. Expresa su intención claramente al lector
4. Elimina elementos innecesarios

## ¿Qué puede ir mal cuando refactorizo?

A parte de unas cuantas cosas que Rainsberger enumera, me quedo con esta
idea: cuando refactorizo, no me permito a mí mismo añadir nuevas funcionalidades
o arreglar bugs.

Tener una hoja de papel y lápiz cerca ayuda a no olvidarse de esas
nuevas funcionalidades o bugs.

## ¿Cuándo debería reescribir en lugar de refactorizar?

Reescribo cuando estoy seguro de que lo voy a poder hacer de forma segura y
de que tengo el suficiente tiempo disponible.

## ¿Cuándo debería dejar el código como está?

Solo cambio código cuando tengo alguna razón para hacerlo. Aunque esto no
significa: [si no está roto, no lo toques].

Si no necesitas arreglar un bug o añadir una funcionalidad relacionada con
ese código, no lo toques.

No refactorices si no tienes un objetivo claro sobre qué aprenderás, qué
vas a añadir o qué vas a arreglar.

## Otras referencias

- [Oxidación del software], de Alejandro Pérez, Autentia
- Martin Fowler acerca de [las 4 reglas de Kent Beck]
- J.B. Rainsberger también habla sobre [los 4 elementos de un diseño simple]

[J.B. Rainsberger]: https://www.jbrains.ca/
[Refactoring: where do I start?]: https://blog.jbrains.ca/permalink/refactoring-where-do-i-start
[Oxidación del software]: https://www.autentia.com/2015/07/22/design-smells-los-malos-olores-motivados-por-la-oxidacion-del-codigo/
[las 4 reglas de un diseño simple]: http://wiki.c2.com/?XpSimplicityRules
[si no está roto, no lo toques]: https://en.wikipedia.org/wiki/Wikipedia:If_it_ain%27t_broke,_don%27t_fix_it
[las 4 reglas de Kent Beck]: https://www.martinfowler.com/bliki/BeckDesignRules.html
[los 4 elementos de un diseño simple]: https://blog.jbrains.ca/permalink/the-four-elements-of-simple-design
