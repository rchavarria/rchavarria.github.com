---
layout: post
title: "La pirámide de tests en la práctica"
date: 2018-12-04 00:00
author: Ruben Chavarria
categories:
- Artículos
- Testing
---

Unas pocas notas sobre un artículo de [Ham Vocke] publicada en la
web de Martin Fowler titulada [The practical test pyramid].

No son notas sobre todo el artículo, porque la mayoría son
conceptos que conozco y estoy de acuerdo, pero alguna idea
nueva sí que he descubierto.

<!-- more -->

El artículo comienza hablando sobre la importancia de los tests y
de su automatización (si lo puede ejecutar la máquina, seguro que
lo hace mejor y más rápido que nosotros).

Continúa hablando de la [pirámide de tests]:

![Tests pyramid](https://martinfowler.com/bliki/images/testPyramid/test-pyramid.png)

*Imagen tomada de la web de Martin Fowler donde habla también
de la [pirámide de tests en inglés]*

Más adelante habla de los tests unitarios:

- Solitarios: donde todos los colaboradores son sustituidos por
[dobles de test]
- Sociales: no todos los colaboradores son sustituidos y algunos
colaboradores son los reales, los de producción

Y cómo no, de los tests de integración. Básicamente habla de tests
que necesitan una base de datos, un sistema de ficheros o un
API REST.

A la hora de probar nuestra aplicación con servicios externos
(servicios que no controlamos nosotros), Ham nos cuenta que podemos
utilizar alguna herramienta, como Wiremock (Java), para simular
un servicio externo. Podemos simular llamadas HTTP,... Son
servicios reales, pero controlados por nosotros, por lo que al
menos controlamos la infraestructura.

El problema de estas herramientas es que, según va pasando el
tiempo, no podemos estar seguros de que nuestro *mock* del servicio
responde de la misma forma que el servicio real.

Para solucionar esto, nos presenta los tests de contrato:

## Tests de contrato

Los sistemas complejos se suelen dividir en varios subsistemas. Algunos
llegan a lo que se conoce como microservicios. En definitiva, servicios
que se comunican a través de REST, RPC, buses de eventos,...

En estos sistemas hay un productor y un consumidor (provider/consumer,
publisher/subscriber,...).

La forma tradicional de testear la comunicación era escribir las
especificaciones en papel (contrato), que la parte productora fuera
implementada y luego se implementaba la parte consumidora. Todos los
problemas aparecían al final, al implementar el consumidor.

La siguiente fase es automatizar esos tests de contrato, con lo que
tenemos que tanto los productores como los consumidores cumplen dicho
contrato, y podemos comprobarlo de forma automática.

Pero hay una alternativa mucho mejor, *tests de contrato dirigidos
por el consumidor*, o tests CDC (Consumer-Driven Contract tests). La
parte consumidora es quien pone las reglas, es quien guía la
implementación del contrato.

El consumidor escribe unos tests automáticos. En ellos se define qué
es lo que necesita el consumidor. Ellos saben qué necesitan, nada
de especificaciones en papel. El productor implementa su parte
de forma que esos tests pasen.

Los tests CDC son una forma automática de hacer que los equipos se
comuniquen y hacen que los interfaces entre equipos (productores y
consumidores) se mantengan funcionando.

[Ham Vocke]: http://www.hamvocke.com/
[The practical test pyramid]: https://martinfowler.com/articles/practical-test-pyramid.html
[pirámide de tests]: http://blog.koalite.com/2014/05/deconstruyendo-la-piramide-de-los-tests/
[dobles de test]: http://xurxodev.com/dobles-de-test/
[pirámide de tests en inglés]: https://martinfowler.com/bliki/TestPyramid.html
