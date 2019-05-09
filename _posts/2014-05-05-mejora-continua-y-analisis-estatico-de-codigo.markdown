---
title: "Mejora contínua y análisis estático de código"
date: 2014-05-05 20:00
author: Rubén Chavarría
comments: true
categories: 
- programming
- continuous improvement
published: true
footer: false
sidebar: true
---

![Evolución del análisis estático de código]({{ site.baseurl }}/assets/images/2014/phpcs-small.png)

En una de las últimas retrospectivas de mi equipo de desarrollo, estuvimos
hablando sobre la mejora contínua, y qué podríamos hacer sobre ella. Afortunadamente
usamos *Jenkins* como servidor de integración contínua y hace ya tiempo configuré
un proyecto en dicha herramienta para realizar análisis estático de código frecuentemente.

Pero hasta ahora no habíamos tomado ninguna decisión sobre qué hacer con ella. Y
en esta retro surgió la oportunidad. 

<!-- more -->

## La herramienta

Como herramienta de análisis estático de código usamos 
[PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer). La razón
principal es que es una herramienta adecuada al lenguaje que queremos analizar, y
existe un proyecto que integra esta herramienta entre otras con Jenkins
([PHP QA Tools](http://phpqatools.org)).

Una vez instalada y configurada, activamos todas las reglas de estilo disponibles
en la herramienta. Estas reglas incluyen comprobaciones para nombrado de funciones,
nombrado de ficheros, uso de constantes en PHP como `true` o `false`, o ciertas
reglas de espaciado: después del nombre de función, alineación del operador de
asignación. Multitud de ellas.

> Si no puedes medirlo, no puedes mejorarlo

## Violaciones del estándar de código

![Descenso del número de errores]({{ site.baseurl }}/assets/images/2014/phpcs-large.png)

En el momento de la conversación sobre la mejora contínua nos encontrábamos en
el máximo que se aprecia en el gráfico, unas 8000 violaciones de reglas de 
estilo.

Y nos pusimos manos a la obra. Después de un pequeño análisis por nuestra parte,
y unos pocos diálogos (la palabra discusiones tiene un pequeño significado de
lucha que no encaja en esta situación), conseguimos bajar ese número a menos de
30. Por lo tanto, está claro que hemos conseguido alguna **mejora**.

## Qué mejoras obtuvimos

En el pequeños análisis realizado por nosotros, descubrimos que algunas reglas de
estilo que teníamos activadas resultaban contradictorias. Mientras que una
obligaba a abrir llaves en la misma línea que la definición de la función:

```php
public function doSomething() {
```

existía otra regla que obligaba a abrir llaves en una línea nueva:

```php
public function doSomething()
{
```

Por lo tanto, una de las dos había que desactivarla, ¿pero cuál?. He aquí la 
verdadera mejora. La mejora no es utilizar una regla u otra, sino alcanzar un
consenso dentro del equipo y decidir qué estilo queremos seguir a la hora de
escribir código. 

Algunas otras reglas nos permitieron detectar qué clases necesitaban ser 
refactorizadas. Por ejemplo, si un método tiene una *complejidad ciclomática*
elevada o si un método está escrito con demasiados niveles de anidamiento.

Otras reglas simplemente nos enfrentaron a la toma de ciertas decisiones:

- Cómo queremos organizar nuestros ficheros
- Cómo queremos dar el nombre a nuestros métodos
- Cómo queremos indentar nuestro código

## Conclusión

No me importa volver a repetirlo, la verdadera mejora no surge de seguir una
regla u otra a la hora de escribir código. La verdadera mejora surge de las
conversaciones, diálogos y *discusiones* entre los miembros del equipo.

¿Y dónde está la parte de *contínua*? Se encuentra en el servidor de integración
contínua. Nuestro código es analizado contínuamente, y en el caso de que haya
un aumento significativo de violaciones de reglas de estilo en nuestro código,
seremos avisados y podremos tomar la decisión sobre si retomamos el control
o lo dejamos para más adelante.

## Referencias

- [Mejora contínua](https://es.wikipedia.org/wiki/Proceso_de_mejora_continua)
- [Integración contínua](https://es.wikipedia.org/wiki/Integraci%C3%B3n_continua)
- [Análisis estático de código](https://en.wikipedia.org/wiki/Static_code_analysis)
(inglés)
