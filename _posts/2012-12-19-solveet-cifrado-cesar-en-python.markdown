---
title: "solveet: cifrado cesar en python"
date: 2012-12-19 12:31
author: Rubén Chavarría
comments: true
categories: 
- solveet
- learning
- programming workout
- python
- tdd
published: true
footer: false
sidebar: true
---

Me gusta resolver problemas de programación regularmente para mejorar como programdor, y para ello uso
la página [Solveet](http://solveet.com). El problema que he solucionado esta semana es el del
[Cifrado César](http://www.solveet.com/exercises/Cifrado-Cesar/145), y está englobado en la iniciativa
[12meses12katas](http://12meses12katas.com/) en la me gusta participar.

El *cifrado César* es muy simple: es un tipo de cifrado por sustitución en el que una letra en el texto
original es reemplazada por otra letra que se encuentra un número fijo de posiciones más adelante 
en el alfabeto.

Decidí usar **python** para este problema porque quería profundizar un poco más en este lenguaje, que lo
tengo muy verde y he escuchado maravillas de él, pero gracias a la solución del problema he aprendido
un par de cosas del lenguaje: uso de la función `map`, y las funciones `str.maketrans` y `str.translate`.

<!-- more -->

## Primera aproximación

Debido a mi poco conocimiento del lenguaje, mi 
[primera aproximación](http://www.solveet.com/exercises/Cifrado-Cesar/145/solution-1076) 
al problema no es muy elegante, y tampoco usa muchas de las fortalezas de python. La verdad es que es
una solución más al estilo de un lenguaje que conozco bastante mejor, Java.

Así pues, una vez publiqué mi solución, decidí echarle un vistazo a soluciones de otros usuarios. 
Encontré varias en python, y de ellas aprendí un par de cosas:

## Uso de la función `map`

Python proporciona la función `map(function, iterable, ...)` 
([documentación](http://docs.python.org/3.3/library/functions.html#map)), la cual llama a la función
`function` para cada uno de los elementos de `iterable` (se pueden usar uno o varios iterables).

En un principio había pensado usar esta función. `function` sería el método que realiza el cifrado
carácter a carácter e `iterable` sería la cadena de texto a cifrar. Pero el método que cifra necesita
otro argumento, el desplazamiento, y no fuí capaz de averiguar por mí mismo cómo pasar este argumento
a mi método usando `map`.

Lo descubrí gracias a la solución de [climens](http://www.solveet.com/exercises/Cifrado-Cesar/145/solution-1052),
y aprovechando lo aprendido, mi solución ahora quedaría así:

``` python
from string import ascii_lowercase as alphabet

def shift(character, offset):
	index = alphabet.find(character)
	if(index < 0): return character
	return alphabet[(index + offset) % len(alphabet)]

def cipher(message, offset):
	ciphered = map(shift, message, [offset] * len(message))
	return "".join(ciphered)

def decipher(message, offset):
	return cipher(message, -1 * offset)

# simple tests
assert "ibm" == cipher("hal", 1)
assert "hal" == decipher("ibm", 1)
```

El *truco* está en que a la función `map` le paso dos `iterables`: la cadena de texto, y un array de enteros
de la misma longitud y cuyos elementos son todos iguales, el desplazamiento. **¡Qué sencillo ahora que lo
sé!**

## Funciones `str.maketrans` y `str.translate`

Desconocía completamente la existencia de estas dos funciones, pero parecen haber sido diseñadas exclusivamente
para el *cifrado César*. Las descubrí gracias a la solución de 
[drabor](http://www.solveet.com/exercises/Cifrado-Cesar/145/solution-1038)

`str.maketrans` ([documentación](http://docs.python.org/3.3/library/stdtypes.html#str.maketrans))
crea un mapa para ser usado en `str.translate` 
([documentación](http://docs.python.org/3.3/library/stdtypes.html#str.translate)), 
y ésta, al ser llamada sobre una cadena de caracteres, devuelve otra cadena donde cada carácter ha sido 
*transladado* según el mapa creado con `maketrans`. 

Ahora sólo hace falta crear el mapa. Uso dos iterables: el alfabeto original, y el alfabeto transladado tantas
posiciones como diga el desplazamiento del cifrado. De esta forma, con desplazamiento `1`, la letra `a` 
corresponderá con la `b` y así sucesivamente. Pero todo ese trabajo lo hará `translate`, no nosotros.

Así queda la solución:

```
from string import ascii_lowercase as alphabet

def cipher(message, offset):
	dictionary_mapping = str.maketrans(alphabet, alphabet[offset:] + alphabet[:offset])
	return message.translate(dictionary_mapping)

def decipher(message, offset):
	return cipher(message, -1 * offset)

# simple tests
assert "ibm" == cipher("hal", 1)
assert "hal" == decipher("ibm", 1)
```

## Conclusión

Cualquiera de las dos soluciones me parece mucho mejor que la mía inicial, y me parecía que debía compartir
lo aprendido al solucionar este problema. 

Y tú, ¿Conoces python? ¿Te apetece participar en [solveet](http://solveet.com)?
¿Tienes alguna sugerencia para mejorar estas soluciones? Deja algún comentario. Si es respetuoso, 
será bienvenido.
