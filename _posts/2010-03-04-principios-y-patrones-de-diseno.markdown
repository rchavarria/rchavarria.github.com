---
title: "Principios y patrones de diseño"
date: 2010-03-04 04:03
author: Rubén Chavarría
categories: 
- java
- software
- patterns
comments: true
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
  <p>Este post pertenece a mi antiguo blog en <a href="http://rchavarria.wordpress.com">wordpress</a>, pero decidí pasarme a github:pages por las siguientes <a href="/blog/2012/12/03/por-que-cambie-mi-blog-en-wordpress-com">razones</a></p>
</div>

Hace tiempo me topé con un documento de Robert C. Martin, de la empresa 
[ObjectMentor](http://www.objectmentor.com) (cuando publicó este material), en 
el cual nos habla de principios de diseño así como de patrones de diseño. El documento 
se titula [Principles and Patterns](http://www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf)
y además de principios y patrones nos habla de los síntomas que nos indican que un 
software se está corrompiendo.

<!-- more -->

Esos síntomas son 4:

1. **Rigidez**: es la tendencia del software a que sea cada vez más difícil realizar un 
cambio. Cada cambio causa una *reacción* en cascada que puede llevar demasiado tiempo 
en completar satisfactoriamente el cambio. Esta rigidez puede llegar a tal extremo que 
el jefe de proyecto *prohíba*, o mejor, *limite*, cualquier cambio 
que no sea crítico. ¿A alguien le suena esta situación?
2. **Fragilidad**: es la tendencia del software en fallar en varios componentes cada vez 
que se realiza algún cambio. Está muy relacionado con la **Rigidez**. 
Si este síntoma empeora lo suficiente, puede hacer que el mantenimiento del software 
sea imposible, porque cada vez que se intente solucionar un problema aparecerán varios 
problemas nuevos
3. **Inmovilidad**: es la incapacidad de reutilizar el código de otros 
proyectos o de otras partes del mismo proyecto. Esto ocurre cuando un módulo que 
deseamos reutilizar tiene tal cantidad de dependencias, que al final decidimos reescribir 
el módulo en lugar de reutilizar el ya existente
4. **Viscosidad**: según Robert, la podemos encontrar de dos formas: 
viscosidad del diseño y viscosidad del entorno. Por viscosidad del diseño se entiende 
que para solucionar un problema, es más fácil solucionarlo por un camino que no sigue el 
diseño que por el camino que nos indica el diseño. Es decir, el diseño hace más complejos 
los cambios que si obviamos el diseño. La viscosidad del entorno es mayor cuanto mayor 
es el tiempo de compilación, despliegue, etc. Esta viscosidad puede llevar a los 
desarrolladores a implementar soluciones no óptimas solamente por ahorrar el tiempo de 
despliegue

En el documento también nos habla de principios relacionados con la programación orientada 
a objetos. Entre estos principios encontramos:

- **Principio Abierto-Cerrado**: un módulo debe estar abierto a extender su 
funcionalidad pero cerrado a modificaciones
- **Principio de sustutución de Liskov**: toda subclase debe ser sustituible 
por su clase base
- **Principio de inversión de dependencia**: que el desarrollo software 
dependa de abstracciones, no de implementaciones
- **Principio de segregación de interfaces**: es preferible tener interfaces 
específicas para cada cliente que una interfaz general para todos ellos

Junto con estos principios, Robert nos presenta otros en cuanto a la arquitectura de 
agrupamiento de las clases que forman nuestro software. Estos principios son de gran 
ayuda al arquitecto sofware y con alguno de ellos nos define ciertas métricas para medir 
la calidad de nuestro código:

- **Principio de equivalencia Reutilización-Release**: la granularidad de 
reutilización se corresponde con la granularidad de la liberación de versiones. Un 
criterio de agrupación de clases en paquetes es la reutilización. Como los paquetes son 
unidades de liberación de versiones, la reutilización se convierte en unidad de liberación 
de versiones
- **Principio de cercanía** (Alguien tiene una traducción mejor para Common 
Closure Principle?): elementos que cambian juntos, deben tratarse como una unidad. 
Aplicando este principio, si agrupamos clases que cambian conjuntamente en paquetes, 
el impacto de liberación de versión a versión tenderá a ser mínimo
- **Principio de reusabilidad común**: elementos que no se pueden reutilizar 
conjuntamente no deben agruparse
- **Principio de dependencia acíclica**: las dependencias entre paquetes no 
deben formar ciclos cerrados
- **Principio de dependencia estable**: las dependencias deben apuntar hacia 
la estabilidad, entendiendo estabilidad como la cantidad de trabajo necesario para 
realizar un cambio. Un buen camino para hacer que un paquete sea difícil de cambiar, es 
hacer que muchos paquetes dependan de él (muchos paquetes inestables dependen de uno 
estable)
- **Principio de abstracciones estables**: los paquetes más estables deberían 
ser los paquetes más abstractos o los que contienen más abstracciones

Una vez vistos estos principios, podemos definir las siguientes métricas:

### Métrica de estabilidad

`I = Ce / (Ca + Ce)`

Donde:

- Ca (Afferent Coupling): dependecias entrantes, es decir, número de clases externas al 
paquete que dependen de clases internas al paquete
- Ce (Efferent Coupling): dependencias salientes, es decir, número de clases internas que 
dependen de clases externas
- I: inestabilidad. Toma valores en el intervalo `[0, 1]`. Cuanto menor sea su valor, 
mayor es la estabilidad del paquete

### Métrica de abstracción (abstractness)

`A = Na / Nc`

Donde:

- Nc: número de clases en el paquete
- Na: número de clases abstractas o interfaces en el paquete
- A: abstracción (abstractness). Toma valores en el intervalo `[0, 1]`

### Métrica de distancia

Representando en una gráfica las dos métricas anteriores (I en el eje de abscisas -x-, A 
en el de ordenadas -y-), obtenemos un gráfico como el siguiente (lo podéis encontrar en 
la página 26 del 
[documento](http://www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf)

![I vs A]({{ site.baseurl }}/assets/images/wordpress/i-vs-a.png)

El lugar óptimo donde nos interesa situar a nuestros paquetes es la línea central, donde 
las dos métricas anteriores están equilibradas. La métrica de distancia nos indica lo 
lejos o cerca que nos encontramos de ella:

`D = | A + I - 1 | / sqrt(2)` con valores en el intervalo `[0, 0.707]`

Si `D = 0`, estamos situados sobre la línea central

**Todas estas métricas miden características de una arquitectura y nos pueden 
ayudar a analizar y cuantificar la estructura de dependencias de una aplicación.**
