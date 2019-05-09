---
layout: post
title: "Leer correos de GMail desde una aplicación Node.js"
date: 2018-03-18 00:00
author: Ruben Chavarria
categories:
- Proyectos
- Node.js
- Lado servidor
---

[Ayuda de GMail para activar POP3](https://support.google.com/mail/answer/7104828?hl=en).

Para leer el correo, se suele usar el protocolo [POP3](https://en.wikipedia.org/wiki/Post_Office_Protocol). En Node.js existen varios paquetes que ayudan en la labor de implementar un *cliente* de correo:

- [Nodemailer](https://nodemailer.com): librería para implementar un cliente y un servidor SMTP ([SMTPConnection](https://nodemailer.com/extras/smtp-connection/) es la parte cliente)
- [node-poplib-yapc](https://www.npmjs.com/package/node-poplib-yapc): Yet another POP3 client library. Parece lo suficientemente guena como para comenzar algo. Muestra un ejemplo mega sencillo que debería funcionar.
- [mailx](https://www.npmjs.com/package/mailx): librería de un cliente POP3. Tiene buena pinta, pero no encuentro nada de TLS en la documentación (al menos a simple vista)

<!-- more -->

## 2018-03-18: Primera prueba con `node-poplib-yapc`

El código se puede encontrar en el repo: [`brthr-email-reader`](https://github.com/rchavarria/brthr-email-reader)

Probando con el código de prueba de la librería, y configurando dirección del servidor, nombre de usuario y contraseña correcta, tengo el siguiente error:

```
events.js:183
      throw er; // Unhandled 'error' event
      ^

Error: [AUTH] Web login required: https://support.google.com/mail/answer/78754
    at Client.onData (/home/rchavarria/projects/brthr-email-reader/node_modules/node-poplib-yapc/main.js:97:10)
    at emitOne (events.js:116:13)
    at TLSSocket.emit (events.js:211:7)
```

Miro en el buzón de correo al que intento acceder, y hay un correo de Google. **Debo permitir acceso a GMail desde aplicaciones no seguras**. Incluyen un [enlace](https://myaccount.google.com/lesssecureapps?rfn=27&rfnc=1&eid=8297942425781677910&et=0&asae=2&pli=1) a la configuración, así que es fácil.

SUCCESS!!

Conseguido!! Leo los mensajes del correo. Los recibo en orden cronológico inverso, el más antiguo primero.

**Problema**: la primera vez recibo todos los mensajes, pero ya no los vuelvo a recibir de nuevo. **Solución**: deshabilitar el acceso POP3 de GMail y volverlo a activar. Es muy pesado, pero bueno. Otra solución es enviarme un correo, de forma que recibiré solamente el nuevo mensaje. Menos pesado.

**¿Qué propiedades tiene cada mensaje?**

Después de conectar el cliente, con `client.retrieveAll` obtengo una lista con todos los mensajes *nuevos* (aquellos que no han sido obtenidos todavía). Pero pasa algo curioso. El primer elemento no es ningún mensaje. Obtengo un elemento más de los mensajes reales, es decir, si hay 3 mensajes nuevos, obtengo un array de 4 elementos. El primero lo tengo que ignorar, al menos por ahora.

Las propiedades son:

- `html`
- `text`
- `headers`
- `subject`
- `messageId`
- `priority`
- `from`
- `to`
- `date`
- `receivedDate`

Las que parecen más interesantes son: `messageId`, `headers` (que contiene mucha información adicional), `from` y `to` (que son objetos en sí).

No veo nada de ficheros adjuntos, que sería interesante. Quizá los adjuntos viajen en las propiedades `text` o `html`.

## 2018-03-18: Leyendo correos con ficheros adjuntos

Aha!!! Un mail con ficheros adjuntos lleva otra propiedad nueva: `attachments` (quién me lo hubiera dicho).

**¿Qué propiedades tiene esa propiedad?**

En realidad es un array de objetos. Cada uno tiene las siguientes propiedades:

- `contentType`: 'text/plain'
- `charset`: 'utf-8',
- `fileName`: 'este-es-un-adjunto.txt',
- `contentDisposition`: 'attachment',
- `transferEncoding`: 'base64',
- `generatedFileName`: 'este-es-un-adjunto.txt',
- `contentId`: 'c7f6a120f330e0eb29c75cba1d10b88a@mailparser',
- `checksum`: '552d08353179c235610a54935d6f24b9',
- `length`: 53,
- `content`: <Buffer ef bb bf 50 72 69 ... >

Bastante directo, y unas propiedades bastante lógicas. El mail de prueba contenía un fichero de texto plano como adjunto, pero el contenido del fichero, presente en `content`, parece que está en un buffer. Supongo que para que pueda contener también contenido binario (imágenes y tal)

**Imprimiendo el contenido de un adjunto**

Con un `attachments[0].content.toString()` tengo esto por consola:

```
Primera línea

Segunda

Tercera

Final-----
```

SUCCESS!!

## Prueba conseguida

Por ahora me doy por satisfecho con esta prueba. ¿Qué he conseguido?

1. Configurar GMail para leer correos en clientes externos a través de POP3
2. Escribir un cliente POP3 que lee correos de GMail
3. Saber la estructura de los correos leidos
4. Leer ficheros adjuntos en los correos, y saber su estructura
5. Imprimir por consola (o guardar en un fichero físico en local) los ficheros adjuntos de los correos recibidos

## Siguientes pasos

- Instalar ESLint como dependencia, para *lintear* el código JavaScript
- Intentar leer todos los correos cada vez, sin tener que desactivar/reactivar POP3 en GMail cada vez
- Estudiar el formato de los archivos adjuntos que voy a tener que parsear
- Configurar Jasmine como framework de tests
- Crear un test que me asegure que los ficheros `src/config/config.js` y `src/config/config.example.js` definen las mismas propiedades. Este sería un test para comprobar que el ejemplo no se me queda desfasado, mientras que tengo la configuración real asegurada en local y sin puchear a GitHub
