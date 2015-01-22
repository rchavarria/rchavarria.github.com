---
layout: post
title: "Calcular hashes MD5 en Dart con cipher"
date: 2015-01-22 23:02
author: Rubén Chavarría
comments: true
categories: 
- dart
- cryptography
published: true
footer: false
sidebar: true
---

Cuando estoy aprendiendo un lenguaje de programación, me gusta practicar
con él, me gusta escribir código con él. Puedes leer los libros o los blogs
que quieras, pero hasta que no escribas aplicaciones y las ejecutes, nunca
apredenderás nada de ese lenguaje.

Para practicar me gusta [Solveet]. Puedes encontrar problemas muy diversos,
tanto fáciles como más complicados. Publicas tu código, con lo que todo el
mundo puede verlo (por eso te esfuerzas en dejar tu código un poquito más
limpio).

Recientemente decidí resolver un problema en el que se trata de escribir
un [acceso a la API pública de Marvel]. Uno de los pasos para acceder a dicha
API es calcular el hash MD5 de unos parámetros a pasar a la API para
autenticarte. Dart es un lenguaje moderno, así que pensé que sería muy
fácil calcular hashes MD5. ¡Menuda decepción me llevé!

<!-- more -->

## Crypto

En realidad no soy ningún experto en Dart, pero no encontré que el lenguaje
proporcionara clases o métodos para hacerlo. Existe una librería llamada
crypto, que parece haber sido escrita por alguien de dentro, pero me
pareció que estaba abandonada y sin documentación (repito, fue una impresión
mía, que me perdone el autor(es)).

## Cipher

Por suerte encontré [cipher], una librería escrita por [Iván Zaera], que me
puso las cosas más fáciles. El repositorio en git parece activo y tiene
una documentación mucho mejor que la de crypto. Al menos encontré la forma
de usar la librería y hacer lo que quería.

Pero no encontré exactamente lo que buscaba, lo encontré algo desperdigado
entre las páginas de la wiki. Así que este post es para mostrar el método
que encontré para **calcular hashes MD5 en Dart con cipher**.

## Código

Para usar la librería, hay que añadir la dependencia de la librería al
fichero `pubspec.yaml` del proyecto:

```
...
dependencies:
    cipher: ">=0.7.1 <0.8.0"
...
```

La siguiente clase, contiene un método público, `digest`, que acepta un
`String` como parámetro y devuelve un `String` con el hash MD5 del mismo:

```
// needs `cipher` as a project's dependency
import 'package:cipher/cipher.dart';
import 'package:cipher/impl/server.dart';
import 'dart:typed_data';
import 'dart:convert';

/**
 * Uses cipher package to compute the MD5 hash of a given String
 */
class Utf8String2MD5 {

    Utf8Encoder encoder;
    Digest md5;

    Utf8String2MD5() {
        // cipher must be initialized before using any class from the package
        initCipher();

        // cipher class to compute the MD5
        md5 = new Digest('MD5');
        encoder = new Utf8Encoder();
    }

    /**
     * @param message Message which MD5 hash will be computed
     * @return the MD5 hash of `message`
     */
    String digest(String message) {
        // get utf-8 values of the message
        List<int> utf8Data = encoder.convert(message);
        // convert to the input data for the cipher class
        Utf8List inputData = new Uint8List.fromList(utf8Data);
        // compute the MD5
        Uint8List digestValue = md5.process(inputData);

        return digestValue
            .map((i) => i.toRadixString(16)) // converts to hexadecimal string
            .map((s) => s.padLeft(2, '0')) // pad strings with 0
            .join(); // join all elements in the List to build a String
    }

}
```

[Solveet]: http://solveet.com
[acceso a la API pública de Marvel]: http://www.solveet.com/exercises/Acceder-a-la-API-Marvel/299
[cipher]: https://github.com/izaera/cipher
[Iván Zaera]: https://twitter.com/izaera

