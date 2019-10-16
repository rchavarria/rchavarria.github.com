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

El artículo expone una serie de beneficios obtenidos a usar TypeScript y unos
costes asociados a lo mismo. Al final, hace un balance de ambos.

<!-- more -->

Para el autor, los puntos fuertes del lenguaje son las herramientas de desarrollo,
la documentación del API que se consigue mediante el tipado, los refactorings y
la sensación de detectar bugs más pronto.

Por otro lado, lo que detecta como costes (contratación de gente, falta de
funcionalidades en el lenguaje, aprendizaje, y el tipado propio del lenguaje) me
parecen bastante genéricos y asociados a bastantes, por no decir todos, los
lenguajes de programación.

En mi opinión, el autor tiene preferencia por *vanilla JavaScript* y su lado
funcional (ya he leído algún artículo suyo en el pasado). Podríamos decir que
TypeScript potencia el lado de la Programación Orientada a Objetos de
JavaScript, así que no va a favorecer a TypeScript. Y el título ya deja entrever
por dónde van los tiros del artículo.

Intenta no dejar bien a TypeScript, pero los malos argumentos, los costes, los
veo aplicables a muchos otros lenguajes. Al final, lo reduce todo al sistema
de tipos, que me recuerda a la lucha Orientación a Objetos Vs Funcional.
 
### Notas

##### Qué me gusta de TypeScript

Los tipos estáticos pueden ser de bastante ayuda para documentar funciones,
clarificar el uso de las mismas y reducir la sobrecarga cognitiva.

Los plugins de TypeScript de los editores de código proporcionan todavía mucha
mejor experiencia de desarrollo que en el ecosistema JavaScript.

##### Retorno sobre la inversion, beneficios

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

##### Costes

**Contratación de desarrolladores**: no todo el mundo está interesado en
TypeScript (el autor recoge datos de la encuesta [The State of JavaScript]).
*Yo veo que eso pasa también con todos los lenguajes, entiendo que no todo el
mundo esté interesado en JavaScript, por lo que no veo que esto sea un problema
específico de TypeScript*.

**Falta de funcionalidades**: faltan algunas funcionalidades como funciones de
orden superior (HOFs), composición, genéricos,...

Para el autor, uno de los mayores costes de TypeScript es que éste no es
*co-expresivo* (si ese término existe) con JavaScript idiomático. Es decir,
TypeScript no te permite utilizar todas las funcionalidad de JavaScript, con lo
que en ocasiones te limita.

En ocasiones, se pierde mucho tiempo intentando tipar cosas que TypeScript no
puede tipar adecuadamente. *Ahora resulta que para el autor, el sistema de tipos
es ahora un coste*.

**Acompañamiento**: sí, es cierto, la gente es productiva con TypeScript más o
menos de forma rápida, pero suele tardar mucho tiempo en tener cierta fluidez
con el lenguaje. *Pero es exactamente como antes, esto pasa con muchos, muchos
lenguajes. Uno puede empezar rápido, pero le cuesta dominarlo*.

Este acompañamiento, esta mentoría, es un efecto secundario de la colaboración,
y es un hábito saludable que ayuda a ahorrar costes a largo plazo.

**Sobrecarga con los tipos**: aquí el autor incluye todo el tiempo extra empleado
en usar tipos, testeándolos, depurándolos y manteniendo las anotaciones de tipos.
*Otra vez, ahora resulta que los tipos son malos*.

También se aprecia un gran aumento de *ruido* en la sintaxis. Este ruido es uno
de los mayores costes de TypeScript, pero se puede mejorar:

- Mejorar el soporte de genéricos usando [higher-kinded types] (*perdón, no tengo
traducción para este concepto*)
- Recomendar definiciones de tipos por separado, no incrustados en la definición
de las funciones (*inline typings*)

##### Conclusiones

TypeScript puede y debería mejorar en inferencia de tipos, funciones de orden
superior y genéricos.

### Referencias

- [The TypeScript tax]
- [Eirc Elliot]
- Encuesta [The State of JavaScript]

[The TypeScript tax]: https://medium.com/javascript-scene/the-typescript-tax-132ff4cb175b
[Eirc Elliot]: https://ericelliottjs.com/
[The State of JavaScript]: https://stateofjs.com/
[higher-kinded types]: https://typelevel.org/blog/2016/08/21/hkts-moving-forward.html
