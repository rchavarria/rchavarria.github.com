---
layout: post
title: "Three great opportunities from legacy code"
date: 2021-03-09 00:00
author: Ruben Chavarria
categories:
- Charlas
- Programacion
- Legacy code
---

Charla de [J.B. Rainsberger][1] titulada [Three great opportunities from legacy code][2]
sobre qué es el *código legado* (legacy code), cómo podemos trabajar con él y
qué podemos aprender de él.

<div style="width: 560px; margin: 0 auto;">
    <iframe width="560" 
            height="315"
            src="https://www.youtube.com/embed/8e9a_b16e7o" 
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
            allowfullscreen>
    </iframe>
</div>

<!-- more -->

Como casi siempre que se habla de *legacy code*, comienza definiendo qué significa
para él este término. Va un poco más allá del típico:

> Código legado es todo aquel que no tiene tests

Y él lo entiende como:

> Código legado es código rentable pero que tenemos miedo a cambiar

Por supuesto, explica con todo detalle su definición:

- Código rentable: código que funciona y por el cual los clientes están dispuestos
a pagar dinero, con el cual se paga el sueldo de todas las personas involucradas
y que mantiene la empresa
- Tenemos miedo...: él lo describe como un sentimiento, como sentir miedo...
- ...a cambiar: ...a producir cualquier cambio en el estado actual del software
o del hardware
  
¿Por qué existe ese *miedo* a cambiar el código? Una de las razones puede ser 
porque no haya ningún test automático (definición clásica de código legado),
o no haya suficientes tests o porque no confiemos lo suficiente en los tests
existentes.

Habla de sentimiento, de miedo a cambiar, porque el código legado suele serlo para
alguien que no está familiarizado con el código. Una vez has trabajado sobre él
durante cierto tiempo, estás más familiarizado con él, y tienes más confianza,
lo conoces mejor, y sientes que puedes cambiarlo de alguna manera.

Comenta algo sobre traer nueva gente a trabajar sobre el código. Esta nueva gente
trae al proyecto: ideas frescas, energía renovada y *frustración renovada*. Y me
hace gracia lo de frustración, porque lo he vivido varias veces, y esa frustración
es energía a querer cambiar y mejorar el software. Lo que nos devuelve otra vez
al sentimiento de cambiar el código legado.

Sobrevivir al código legado:

1. Rescatar el código: perder ese miedo a cambiarlo, ser capaz de mejorarlo poco
a poco y poder arreglar bugs e implementar nuevas funcionalidades
2. Organizar el trabajo
3. Navegar la gente involucrada

Conflicto principal del código legado:

> Es como la pescadilla que se muerde la cola. Quiero refactorizar para mejorar
> la calidad del código. Para refactorizar de forma segura, necesito tests.
> Pero para añadir tests necesito modificar el código un poco, refactorizar. Pero
> para hacerlo necesito tests. Pero...

¿Cómo rompemos ese círculo? Para romperlo, mucha gente (incluído él mismo) se ha
enfocado demasiado en los tests. Es una solución lógica, técnica, que a los
programadores nos gusta. Pero genera demasiados conflictos en el proyecto

J.B. propone otras técnicas. Una de ellas es lo que llama *microcommits*, es
decir, hacer commits muy muy pequeñitos, absurdamente pequeños. Teniendo muchísimos
puntos de referencia, te va a permitir repetir los tests (quizá manuales) muy
rápidamente. Vas a poder tener una máquina del tiempo para detectar a partir de
qué punto tus cambios fueron demasiado agresivos y rompiste el código. Podrás
ir adelante y atrás en tus cambios, pasito a pasito, con cambios tan pequeños
como los commits que hayas hecho y probarlos. Podrás olvidarte de hacer el trabajo
(porque ya lo has hecho) y centrarte en qué cambios son válidos y qué cambios
no lo son.

Otra forma de romper el círculo es refactorizar de forma segura, hacer cambios
tan pequeñitos en el código que sea *imposible* equivocarse. Así que, practica
tus habilidades de refactorizar en cualquier situación, especialmente en aquellas
donde no sea crítico, para que estés muy acostumbrado a hacerlas en las situaciones
complicadas.

> Practica en entornos controlados, para sentir confianza en situaciones críticas

Practicando en entornos controlados, podrás beneficiarte de lo que los psicólogos
llaman **chunking** (ni idea del término en español, sería algo así como crear
abstracciones de conocimiento, el concepto lo vi en el curso [Aprendiendo a
aprender][3])

La idea es empezar a practicar prestando atención hasta al más mínimo detalle.
Según pasa el tiempo, automatizarás más y más detalles. Podrás prestar más atención
a detalles de más alto nivel. Estarás construyendo bloques, cada vez más complejos,
pero no tendrás que prestarles atención. Si todo esto lo haces en un entorno o
proyecto controlado, conseguirás hacer esas tareas con mucha más confianza cuando
lo necesites en la vida real.

**Organiza cuidadosamente tu trabajo**. No debes pedir permiso para organizar tu
propio trabajo. Organiza tus pensamientos. Toma notas. Haz que esa información
sea fácil de buscar: texto plano, sitio web, centralizado,... Practica
identificando y resolviendo problemas en el trabajo (open loops los llama).
Experimenta con **monotarea**, dedícate a una sola cosa cada vez. Escribe tutoriales
para resolver problemas que te encuentras en el trabajo. Compártelos luego con 
tus compañeros.

Habla sobre unas cuantas técnicas de productividad personal: Getting Things Done,
monotasking, inbox zero, pomodoro,...

**Trabaja mejor con los demás**. Tener herramientas para gestionar el estrés es
muy importante mientras trabajas con código legado.

Habla sobre un modelo mental para *depurar* las relaciones con los demás. Muchos
de los problemas se deben a cómo interpretamos nosotros las reacciones de los
demás. Debemos darnos cuenta de cómo reaccionamos nosotros a las interpretaciones
que hacemos de las comunicaciones de los demás.

En resumen:

1. Practica diseño evolutivo: refactoring, TDD
2. Organiza tu trabajo: getting things done,...
3. Gestiona tu estrés y emociones: medita, comunicación no violenta,...
4. Practica empatía y compasión hacia los demás

### Conclusión

Todas las charlas de J.B. Rainsberger son bastante interesantes, así como los
artículos de sus blogs. El contenido que publica suele estar centrado en tests,
TDD, Agile y otros temas relacionados con la calidad del código.

En esta charla habla de algunas oportunidades que nos brinda el código legado
para gestionarlo mejor, trabajar con él y mejorar como profesionales.

Habla de tres conceptos:

1. Rescatar el código: perder el miedo a cambiarlo, mejorarlo poco a poco a través
del diseño evolutivo, refactorings, TDD y otras técnicas
2. Organizar tu propio trabajo: vaciando la mente, tomando notas y otras técnicas
de mejora personal
3. Interaccionar con la gente involucrada: comunicación no violenta, gestionar
el estrés...

### Referencias

- [Diseño evolutivo][4]
- [Getting Things Done][5]
- [Satir Interaction Model][6]: para comprender cómo nos relacionamos con los demás
- [Don't let misscomunication spiral out of control][7]: un artículo bastante
antiguo donde J.B. Rainsberger ya habla del modelo de interacción de Satir

[1]: https://www.jbrains.ca/
[2]: https://www.youtube.com/watch?v=8e9a_b16e7o
[3]: {{ site.baseurl }}{% post_url 2017-01-04-learning-how-to-learn %}
[4]: https://tdd.training
[5]: http://link.jbrains.ca/getting-started-with-gtd
[6]: https://katrinatester.blogspot.com/2014/10/satir-interaction-model.html
[7]: https://www.infoq.com/articles/satir-communication-model-teams/
