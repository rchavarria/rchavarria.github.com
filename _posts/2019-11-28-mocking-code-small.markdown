---
layout: post
title: "Notas sobre el artículo: Mocking is a code smell"
date: 2019-11-28 22:28
author: Ruben Chavarria
categories: 
- Artículos
---

Comentarios sobre el artículo [Mocking is a code smell], escrito por [Eric Elliot],
un conocido por aquí.

El artículo expone ...

Me recuerda de alguna manera al artículo de [James Shore] sobre [patrones para
no mockear].

<!-- more -->

ESCRIBE POR AQUI TU CONCLUSION Y OPINIÓN SOBRE EL ARTÍCULO
 
### Notas

Algunos proyectos, para poder utilizar mocks en sus aplicaciones, envuelven
sus unidades, sus componentes, con funciones para inyectar dependencias. O peor,
empaquetan servicios en contenedores de inyección de dependencias (como lo
hace Angular).

La inyección de dependencias no es la mejor forma de conseguir desacoplamiento.

##### TDD debería llevar a un mejor diseño

Si te encuentras con que tu código es más difícil de leer y mantener cuando lo
haces testeable, o si tienes que inflar tu código con código repetitivo para
inyección de dependencias, entonces estás haciendo TDD mal.

Escribir código más testeable debería hacerlo más sencillo.

##### ¿Qué es un olor en el código?

Si no hay lógica en tu código, sólo *pipes* y composiciones de funciones puras,
0% de cobertura de tests puede ser lo aceptable. En cambio, si hay lógica
(condicionales, asignaciones a variables, llamadas a funciones,...), seguramente
sí necesitas algún tipo de cobertura.

##### ¿Qué es un mock?

Todos los dobles de test representan código real del que depende la unidad que
estamos probando, por lo tanto, todos los dobles de tests son una indicación
de acoplamiento en el código.

##### ¿Qué es la cobertura de tests?

Debido a que los casos de uso pueden involucrar entorno, varias unidades o
componentes, usuarios, condiciones de red,... es imposible cubrir todos los
casos de uso sólo con tests unitarios.

##### ¿Qué es un fuerte acoplamiento?

Si estamos mockeando algo es porque las dos unidades están acopladas, luego
puede haber una oportunidad de hacer nuestro código más flexible si reducimos
el acoplamiento entre ellas, y así eliminar los mocks.

Habla de varias formas de acoplamiento, todas ellas me recuerdan a varios tipos
de [connascence] (lo siento, no tengo ni idea de cómo se podría traducir el
término).

##### ¿Qué causa el acoplamiento?

Habla de mutabilidad, efectos colaterales, sobrecarga de responsabilidades,
instrucciones procedurales, composición imperativa. Muchos de estas causas
se *solucionan* con programación funcional.

##### ¿Cómo se relacionan la composición y los mocks?

La esencia de todo desarrollo software es el proceso de romper un problema grande
en problemas más pequeños e independientes (descomposición) y unir las soluciones
para formar una aplicación que soluciona el gran problema original
(composición).

Los mocks son necesarios cuando las unidades en las que se ha dividido el gran
problema dependen las unas de las otras. Así pues, nuestra estrategia ha fallado
al descomponer en problema en unidades más pequeñas e independientes.

##### ¿Cómo eliminamos el acoplamiento?

**Usando funciones puras**

Las funciones puras no modifican variables globales, parámetros pasados, red,
disco o la pantalla. Sólo deben devolver un valor.

Pueden ser *memoized* (se pueden cachear los valores devueltos), porque para los
mismos valores de entrada, siempre tendrá los mismos valores de salida. La
función pasa a ser como una tabla clave-valor.

**Aislar los efectos colaterales de tu lógica**

1. Usando pub/sub para desacoplar entrada/salida de las vistas y la lógica. Ejemplos
son el DOM, añadiendo listeners a eventos; y Redux, que envía *actions* para
actualizar el estado global.
2. Aislar la lógica de la entrada/salida: en ciertas ocasiones, la lógica
condicional se puede eliminar porque construcciones del lenguaje, como las
promesas en JavaScript, vienen con cierta forma de toma de decisiones (control
de errores,...). Escribiendo pequeñas funciones que se puedan encadenar (mediante
*pipes*), se pueden testear independientemente sin mockear el resto.
3. Usar objectos que representan computaciones futuras: es la estrategia utilizada
por Redux. Usar generadores en JavaScript como una forma de componer las funciones,
como una forma de ejecutarlas en el futuro.

##### Los mocks no son malos del todo

> Los olores en el código son señales de advertencia, no leyes

Mockear viene genial para los tests de integración

A veces te gustaría testear cómo tus componentes se comunican con una API de
terceros, y esa API es prohibitiva económicamente.

Es imposible llegar al 100% de cobertura sin tests de integración.

### Conclusiones

### Referencias

- Artículo: [Mocking is a code smell]
- [Eric Elliot]

[The TypeScript tax]: https://medium.com/javascript-scene/the-typescript-tax-132ff4cb175b
[Eric Elliot]: https://ericelliottjs.com/
[James Shore]: 
[patrones para no mockear]: 
[connascence]: 
