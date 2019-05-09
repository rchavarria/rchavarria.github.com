---
layout: post
title: "Real Software Engineering"
date: 2019-01-02 00:00
author: Ruben Chavarria
categories:
- Charlas
- Ingeniería de Software
---

Charla de [Glenn Vanderburg] titulada [Software Art Thou, real software engineering]
sobre qué es ingeniería y cómo vemos la ingeniería en el mundo del software.
Similitudes y diferencias con otras ingenierías y discusiones sobre si desarrollar
software es o no una ingeniería de verdad.

En realidad, creo que esta es la segunda vez que veo la charla, pero no encuentro
las notas por ningún lado, así que ahí van.

Como bonus, van las notas de una charla parecida del mismo autor hablando sobre
Ingeniería y Artesanía del Software.

<!-- more -->

Comienza diciendo que todos los *problemas* vienen por dos ideas, que básicamente se
pueden fundir en una

> La idea que tenemos de una Ingeniería no nos cuadra al 100% con lo que vemos que es
el desarrollo de software

Pero es que ninguna otra disciplina, que consideramos ingeniería, lo cumple tampoco al
100%.

Hace una distinción entre dos Ingenierías de Software: la *Académica* y la
*Mainstream*. La académica, allá por los años 60-70, intentó parecerse a otras ingenierías.

Esta es la visión que tiene el autor:

1. El desarrollo de software **es** un campo de ingeniería
2. Siempre ha sido así
3. El modelo *Rational* (modelo como se supone que debería funcionar una ingeniería, mucha
documentación, mucho análisis y poca construcción) es una caricatura de cómo funcionan
las ingenierías
    . Ninguna rama de ingeniería funciona realmente como dice este modelo
    . Algunas ramas de ingeniería de *toda la vida* no se parecen en nada a lo descrito
    aquí
4. No necesitamos convertirnos en ingenieros, necesitamos seguir refinando nuestra
disciplina de ingeniería (como hacen el resto de ramas)

Luego pasa a hablar de los errores de la Ingeniería Académica de Software. De las
conferencias donde apareció el término por primera vez, de cómo había intereses
escondidos para engatusar a la OTAN, de cómo se ignoraron ciertas voces críticas,
el modelo *Rational*, de cómo se enfatizó demasiado que el software fuera correcto
(demasiado análisis) frente a los costes de realizarlo.

Luego, pasa a hablar de lo que realmente es la ingeniería, y de que hay pocos libros o
recursos dedicados a la ingeniería en sí. Define dos modelos de procesos de control

1. Definido: requiere que toda parte del trabajo sea entendida, se obtienen siempre
los mismos resultados
2. Empírico: ejercita el control a través de inspección frecuente y adaptación a
procesos imperfectos que generan resultados impredecibles y no repetibles

Compara diversos campos de la ingeniería con estas definiciones:

Definido -> Civil -> Estructural -> Mecánica -> Aeroespacial -> Química
-> Eléctrica -> Industrial -> Software

> Engineeringn is a creative pursuit

Los ingenieros adoptaron métodos formales (modelos matemáticos,...) para poder
ahorrar dinero.

Los ingenieros son practicantes, no teóricos. Y evolucionan en base a sus
prácticas

Vale, entonces, después de todo eso, ¿qué es ingeniería del software?

Aquí compara la economía de contruir un edificio (donde lo caro es construir y lo
barato es diseñar) con la de desarrollar un software (donde lo barato es construir
- compilar y tal- y lo caro es diseñar - escribir el código - )

Habla de prácticas descritas en Extreme Programming, relacionándolas
con trabajos de ingeniería, que aplican a distintos niveles a la hora de diseñar
y escribir software, así como a distintas escalas de tiempo.

### Craft, Engineering, and the Essence of Programming

Muy parecida a esta charla, Glenn tiene otra:
[Craft, Engineering, and the Essence of Programming](https://www.youtube.com/watch?v=LlTiMUzLMgM)

En ella termina hablando de si los ingenieros de software son en realidad
Ingenieros o Craftsmen. Al final, se monta su historia para concluir que 
son ambos.

En la charla, la idea principal con la que me quedo es:

> Cuanto más abstracta es la rama de la ingeniería, más concreto es el modelo
con el que trabaja

Al igual que en la charla anterior, hace una pequeña clasificación, ordenando
algunas ingenierías de más concretas (que trabajan con cosas físicas) a más
abstractas (trabajan con menos cosas físicas y más cosas abstractas). Repito
esta clasificación:

Civil -> Estructural -> Mecánica -> Aeroespacial -> Química
-> Eléctrica -> Industrial -> Software

En Ingeniería de Software, la más abstracta de todas, su modelo es el más concreto.
Su modelo es el código, que también es el diseño. De hecho, el modelo (el código)
es tan concreto que los ingenieros *sienten* que están trabajando con el
producto final, con el resultado final, cuando están diseñando el modelo.

Las últimas palabras son para la Artesanía del Software (Craftsmanship) en
comparación con la Ingeniería del Software:

> Dado que trabajamos con información pura, con pura abstracción. Dado que
somos escritores, somos creadores y diseñadores, tenemos el lujo de ser tanto
ingenieros como artesanos. Somos diseñadores y *hacedores*. No estamos
aislados de los artefactos que diseñamos, y al igual que los artesanos, podemos
sentir lo que construimos y su calidad nos afecta emocionalmente. Tenemos ese
lujo, pero también tenemos la responsabilidad de no ser solamente artesanos,
si no también ingenieros. Porque de otra forma, tenemos que ser artesanos y no
solamente ingenieros. Es un lujo y una responsabilidad, porque si no, perderíamos
inevitablemente la visión de los aspectos menos tangibles, que no menos
importantes, de nuestras creaciones.

### Algunos libros

- The design of design, de Gordon L Glegg
- Definition of the engineering method, de Bill Vaughn Koen
- To engineer is human, de Henry Petroski
- What engineers know and how they know it, de Walter G. Vincenti (aeronaútica)
- The existential pleasures of engineering, de Samuel C. Florman

[Glenn Vanderburg]: https://vanderburg.org/
[Software Art Thou, real software engineering]: https://www.youtube.com/watch?v=RhdlBHHimeM
