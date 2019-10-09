---
layout: post
title: "Notas sobre el artículo: TypeScript tax"
date: 2019-02-15 23:23
author: Ruben Chavarria
categories: 
- Artículos
---

Comentarios sobre el artículo [The TypeScript tax], escrito por [Eric Elliot], un
fuera de serie.

<!-- more -->

foo bar foo bar

> lorem impsum

<!-- -->

> dolor sig amet

blah blah

### Notas

##### Qué me gusta de TypeScript

Los tipos estáticos pueden ser de bastante ayuda para documentar funciones,
clarificar el uso de las mismas y reducir la sobrecarga cognitiva.

Los plugins de TypeScript de los editores de código proporcionan todavía mucha
mejor experiencia de desarrollo que en el ecosistema JavaScript.

##### Retorno sobre la inversion

El análisis de beneficios Vs costes que hace el autor le da un probable ROI
negativo a TypeScript

**Herramientas de desarrollo**: reduce la carga cognitiva de los desarrolladores
al proporcionar consejos sobre tipos e información sobre posibles errores en
tiempo real, según vamos programando. Pero JavaScript también puede conseguir
algo parecido, aunque haya que trabajárselo un poco.

TypeScript no compite contra JavaScript a pelo, sino con todo un ecosistema de
herramientas alrededor del lenguaje: autocompletado, inferencia de tipos,
linters, funcionalidades de ECMAScript 6 en adelante,...

El autor sugiere usar parámetros por defecto para reducir las anotaciones en el
código TypeScript para reducir la sobrecarga introducida por los mismos. Los tipos
es uno de los costes añadidos por el lenguaje. Pero los parámetros por defecto
pueden ser usados en JavaScript también.

**Documentación del API**: uno de los beneficios de TypeScript es la mejor
documentación para APIs que siempre está sincronizada con tu código fuente.

Esto sería una gran diferencia, pero en JavaScript existen multitud de generadores
de documentación. *Sí, pero no viene dado por el lenguaje, es algo que tienes
que configurar tú. Hmmm, para mí TypeScript tiene más ventaja aquí de lo que
transmite el autor*.

**Refactorings**: si obtienes un gran beneficio de TypeScript en tus 
refactorizaciones, suele ser un *mal olor* indicando que tu código está altamente
acoplado. *Pero eso será malo en JavaScript igualmente, no veo por qué el autor
lo considera solo malo para TypeScript*.

**Seguridad de tipos**: no hay mucha evidencia de que los tipos ayuden a 
disminuir drásticamente el número de bugs. Otras prácticas (TDD, programación
por parejas,...) sí que lo hacen, pero son más complicadas de llevar a cabo.

Algunos comentan que con TypeScript puedes obtener información sobre algunos tipos
de bugs en tiempo real, pero eso es algo que también se puede lograr con 
herramientas de inferencia de tipos.

Las mayores fuentes de bugs en el software, de lejos, son los fallos a la hora
de definir el comportamiento que realmente se quiere de él o implementar
correctamente la especificación.

Teóricamente, TypeScript puede detectar hasta un 20% de los posibles bugs. Eso
es un montón, pero no parece que sea lo suficiente. Los errores de tipado son
sólo un pequeño conjunto de todos los posibles errores, y existen otros métodos
de detectar errores de tipado.

### Referencias

- [The TypeScript tax]
- [Eirc Elliot]

[The TypeScript tax]: https://medium.com/javascript-scene/the-typescript-tax-132ff4cb175b
[Eirc Elliot]: https://ericelliottjs.com/
