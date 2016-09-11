---
layout: post
title: "Elixir: quinto asalto"
date: 2016-09-11 11:43
author: Ruben Chavarria
comments: true
categories: 
- learning
- elixir
published: true
footer: false
sidebar: true
---

Y ya vamos por el quinto asalto, el quinto de la serie sobre el aprendizaje del
lenguaje [Elixir]. En este asalto aprenderemos estructuras de control de flujo,
esenciales en cualquier lenguaje de programación. No sé en otros lenguajes
funcionales, pero en Elixir, estas estructuras no son muy bien acogidas. De
todas formas, son parte del lenguaje, son sencillas y nos servirán para
establecer conexiones con lenguajes que ya conozcamos.

Para seguir con el aprendizaje, sigo con el método seguido en otros asaltos
partiendo del post [aprendiendo Elixir]:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

{% img right /images/2016/fight-II-harc-II.jpg %}

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/6bQhPq">Fight II / Harc II</a> de <a href="https://www.flickr.com/photos/silangel/">silangel</a>, <a href="https://creativecommons.org/licenses/by-nc/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by/2.0/">CC BY 2.0</a>
  </span>
</div>

<!-- more -->

## Aprender lo suficiente para comenzar

En Elixir no se usan mucho, se suelen escribir métodos pequeños, que junto con
claúsulas de guarda y *pattern matching* nos alejan bastante de lo que aquí
estudiaremos. Normalmente, se suelen favorecer esos mecanismos frente a
estructuras de control. Al principio cuesta acostumbrarse, pero luego uno se va
dando cuenta de que los cuerpos de los métodos quedan más pequeños y más
enfocados a hacer una sola cosa, aunque despista un poco que una misma función
tenga varios cuerpos.

**`if` y `unless`**

```
# Ambos toman dos parámetros, una condición y una *keyword list*, cuyas claves posibles son `do:` y `else:`.
if 1 == 2, do: "truthy", else: "falsy"
unless 2 == 1, do: "do not execute", else: "execute this"

# igual que las funciones, se puede acortar un poco
if 1 == 2 do
  "truthy"
else
  "falsy"
end
```

**`cond`**

En realidad es una macro, como muchas otras construciones del lenguaje, y
acepta una serie de condiciones. Se ejecutará el código de la primera condición
que se evalúe a `true`.

```
# Resolver la kata FizzBuzz
cond do
  rem(current, 3) == 0 and rem(current, 5) == 0 -> "FizzBuzz"
  rem(current, 5) == 0 -> "Buzz"
  rem(current, 3) == 0 -> "Fizz"
  true -> current
end
```

En muchos casos, una mejor alternativa puede ser utilizar múltiples funciones,
pattern matching y claúsulas de guarda en lugar del bloque `cond`.

**`case`**

`case` permite evaluar una serie de patrones, y ejecuta el código asociado a
dicho patrón. También se pueden usar claúsulas de guarda.

```
# para controlar errores al abrir un fichero
case File.open("some file.txt") do
  { :ok, file } -> IO.puts "First line: #{IO.read(file, :line)}"
  { :error, reason } -> IO.puts "Failed to open file: #{reason}"
end

# con claúsulas de guarda
dave = %{name: "Dave", age: 27}
case dave do
  person = %{age: age} when is_number(age) and age >= 21 -> IO.puts "You are allowed #{person.name}"
  _ -> IO.puts "You are not allowed"
end
```

**Excepciones**

Las excepciones en Elixir se usan para casos excepcionales. Por ejemplo, si hay
un fallo al leer un fichero de configuración, con un nombre fijo. Pero no si
hay un error al leer un fichero que el usuario ha introducido el nombre,
podemos controlar eso, y no sería un error excepcional.

```
# lanzando una RuntimeError
raise "Giving up"

# o con algunos argumentos
raise RuntimeError, message: "Stack overflow"

# por convención, se suele escribir `!` al final de una llamada que puede
# devolver una excepción bien conocida, por ejemplo
{ ok: file } = File.open!("foo.bar")
```

## Aprender lo suficiente para hacer algo de utilidad

- [exercise-01-round-05.exs]: reescribe la kata FizzBuzz con `case`
- [exercise-02-round-05.exs]: muchas funciones tienen una segunda
  implementación, que termina con `!`, la cual, si el resultado no coincide con
`{ :ok, data }` lanza una excepción. Implementa una función `ok!` que haga
exactamente esto

## Enseñar lo aprendido, y repetir desde el paso 7

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta
el siguiente asalto.

[Elixir]: http://elixir-lang.org/
[aprendiendo Elixir]: /blog/2016/01/17/aprendiendo-elixir/
[exercise-01-round-04.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-05/exercise-01-round-05.exs
[exercise-02-round-04.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-05/exercise-02-round-05.exs

