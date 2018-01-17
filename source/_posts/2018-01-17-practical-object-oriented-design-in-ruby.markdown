---
layout: post
title: "Practical Object-Oriented Design in Ruby"
date: 2018-01-17 22:03
author: Ruben Chavarria
comments: true
categories: 
- personal
- book reviews
- programming
- design
published: true
footer: false
sidebar: true
---

##### de Sandi Metz

{% img left /images/2018/poodr.jpg 250 323 %}

### Por qué lo he leído

Éste es un libro que lo recomienda mucha gente cuando se habla de *programación
orientada a objetos*, es muy mencionado en conversaciones por twitter y el
mundo online. Pero la guinda del pastel vino cuando ví que lo recomendaba
[Carlos Blé] en su blog. Entonces supe que era una lectura obligada.

<!-- more -->

### De qué trata el libro

Va sobre programación orientada a objetos. Normalmente, al hablar de POO, no se
avanza mucho más allá de herencia y polimorfismo. Sandi va muchos pasos más
allá. Explica la POO desde un punto de vista un poco diferente, donde los
objetos no son el centro del paradigma, si no los mensajes que se intercambian
entre ellos.

Por supuesto, el libro también habla de herencia, de cuándo usarla y cuándo no.
Habla de composición, comparándola con la herencia. Y habla de otras formas de
reutilizar o compartir el código.

Por último, habla sobre cómo gestionar los tests de nuestra aplicación
manteniendo unos costes de desarrollo bajo control.

### Conclusiones y valoración

Es curioso que para describir el paradigma de la programación orientada a
objetos no se centre en objetos, si no en los mensajes que deben pasarse entre
ellos. Es un cambio de punto de vista, y me gustaría poder interiorizarlo
fácilmente, pero no me resulta así. Es un esfuerzo que debo hacer y que seguro
que merecerá la pena.

Aunque centrado en Ruby, describe otras formas de reutilizar código aparte de
la herencia y la composición. Les llama módulos, o roles. En otros lenguajes
existen conceptos similares, como los *traits* en PHP o los *mixins* en
JavaScript. No creo que se puedan aplicar a todos los lenguajes de
programación, pero si a la mayoría de los lenguajes dinámicos.

En cuanto a la valoración, coincido con muchísima gente: este libro puede ser
un antes y un después en la comprensión de la Programación Orientada a
Objectos, sobre todo por el punto de vista tan diferente a la hora de
entenderla. Envío de mensajes, envío de mensajes, envío de mensajes,...

### Qué he aprendido

Impresionante ver cómo refactoriza una herencia a una composición de objetos:
engloba una colección de objetos en una nueva clase, crea una factoría que crea
cada una de las partes, simplifica las partes como dadas de configuación. De
esta forma, añadir un nuevo tipo no requiere una nueva clase, solamente nueva
configuración

Diseñar basado en mensajes crea aplicaciones más flexibles que diseñar pensando
en objetos. En lugar de preguntarte: tengo un objeto ¿qué debería hacer?,
deberías preguntarte tengo un mensaje, ¿a quién se lo envío? No hay que
centrarse en los objetos de dominio, si no en los mensajes que se pasan entre
ellos.

Eligiendo relaciones (herencia, roles/*duck typing*, composición)

1. Herencia para relaciones *es-un* (is-a). Especialmente si la jerarquía es
   estrecha y tiene pocos niveles
2. Role/duck type para relaciones *se-comporta-como* (behaves-like-a). Donde
   varios objetos no relacionados se quieren comportar del mismo modo
3. Composición para relaciones *tiene-un* (has-a). Un objeto tiene varias
   partes pero es más que la suma de ellas, si no sería una colección y ya está

Para obtener el máximo valor de los tests, hay que tener el mínimo de ellos.
Para ello, hay que testear cada cosa una sola vez, y en el lugar apropiado.

1. Mensajes entrantes tipo *query* hay que testear el **estado** que devuelven
2. Mensajes salientes tipo *command*, hay que testear que son llamados, cuantas
   veces y con qué parámetros
3. Mensajes salientes tipo *query*, no se testean (ya los testearán los tests
   de otro objeto)

### Frases que me gustaría recordar

> Siempre existe una tension entre mejorarlo ahora o mejorarlo después. Un buen
> diseñador sabe minimizar los costes tomando decisiones valorando lo que sabe
> ahora y lo que sabrá en el futuro, porque nunca sabrás menos de lo que sabes
> hoy

<!-- more -->

> Gestiona la dirección de las dependencias: depende de cosas que cambien menos
> frecuentemente que tú. Para conocer las dependencias más interesantes nos
> fijamos en 3 aspectos: probabilidad del cambio, nivel de abstracción y número
> de dependencias (sobretodo de la 1ª y 3ª)

<!-- more -->

> Las cosas que una clase conoce conforman su **contexto**, lo cual tiene un
> efecto directo en lo fácil o difícil que es reusar (y por tanto testear) esa
> clase

<!-- more -->

> Para que una herencia funcione, debe de haber una relación de
> generalización-especialización, donde la especialización sea todo lo general
> y algo más

<!-- more -->

> La regla general de refactorizar a una herencia es colocar el código de tal
> forma que haya que promocionar abstracciones a las superclases, en lugar de
> *rebajar* concrecciones a las subclases

<!-- more -->

> Si hay código que pregunta por el tipo de un objeto para enviar un mensaje u
> otro, estamos necesitando *duck typing*, una abstracción. Cuando además del
> interfaz (*duck type*) necesitamos compartir comportamiento, necesitamos un
> *role* (módulo, trait, mixing,...)

<!-- more -->

> La composición es otra forma de organizar el código donde cada parte es más
> independiente, pero no tenemos delegacion automática de mensajes, si no que
> hay que hacerlo de forma explícita

<!-- more -->

> Código creado con composición es *transparente* (T de *true*), suelen ser
> clases pequeñas con una única responsabilidad y suele ser fácil entenderlas.
> Son *usables* (U de *true*) porque son pequeños y enfocados. Son *razonables*
> (R de true) porque se pueden extender sin modificar

### Recursos relacionados

- El resto de [notas sobre POODR]

[Carlos Blé]: https://twitter.com/carlosble
[notas sobre POODR]: https://github.com/rchavarria/blog-post-incubator/blob/master/published-book-notes/practical-object-oriented-design-ruby-by-sandi-metz.markdown

