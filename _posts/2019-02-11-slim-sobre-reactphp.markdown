---
layout: post
title: "Implementar un API REST sobre ReactPHP"
date: 2019-02-11 00:00
author: Ruben Chavarria
categories:
- REST
- Integraciones
---

Necesito implementar una nueva funcionalidad para un proyecto que tengo
entre manos.

Tengo un *Sistema de Notificaciones*, escrito en PHP, cuyo único acceso desde
el exterior es a través de conexiones [WebSocket] implementadas en una
aplicación que llamaré simplemente *Servidor*. Los clientes de este
sistema son aplicaciones web que crean una conexión permanente desde el
navegador y mediante la cual reciben notificaciones de distinto tipo.

Necesito acceder al sistema a través de un API REST, para poder hacer
peticiones al sistema y extraer así cierta información: monitorización,
configuración,...

![Sistema de Notificaciones]({{ site.baseurl }}/assets/images/2019/sistema-notificaciones.jpg)

<!-- more -->

# El problema

En principio no debería haber ningún problema para crear un API REST.
La librería [Slim] es una gran conocida en el mundo PHP, y permite
crear APIs REST de una forma tremendamente sencilla.

Entonces, ¿cuál es el problema? Esta API va a tener que comunicarse de
alguna forma con los subsistemas dentro de mi Sistema de Notificaciones,
y sobretodo con el Servidor.

Para comunicar estos subsistemas, utilizo mensajes distribuidos, ayudado
de la librería [ZeroMQ][3]. Esta librería me permite implementar diversos
patrones para comunicar aplicaciones y funciona realmente bien.

Así que, mi API debería poder comunicarse con el resto de subsistemas,
pero un API REST no tiene la misma filosofía que mis otros subsistemas.
Podríamos decir que un API REST sólo ejecuta código cuando recibe una
petición, sólo se *activa* ante una petición de un cliente. El resto del
sistema está continuamente ejecutándose y haciendo tareas. Al contrario
que la API que estaría continuamente esperando nuevas peticiones.

¿Cómo consiguen esos subsistemas estar haciendo tareas contínuamente?
Por que PHP es un lenguaje muy orientado a la filosofía de
petición/respuesta. Pues lo consiguen gracias a [ReactPHP], una librería
para aplicaciones *reactivas* en PHP, es decir, aplicaciones que
responden a eventos, y no necesariamente sólo a eventos de conexiones
de clientes.

De esta forma puedo realizar tareas periódicas, o responder cuando
un subsistema recibe un mensaje de otro subsistema.

Al final, el problema técnico a solucionar se resume en: debo conseguir
integrar Slim y ReactPHP. Después, también sobre ReactPHP, implementaré
la comunicación del API con los subsistemas que lo necesiten.

# La solución

Como ya he dicho antes, Slim no está pensado para aplicaciones 
asíncronas/reactivas (responder frente a mensajes llegados de otras
aplicaciones, por ejemplo), por lo que no es un problema muy 
documentado.

Aún así, he conseguido encontrar un par de proyectos en los que me he
podido basar para solucionar este problema.

1. [reactphp-slim]: promete bastante al principio, pero usa versiones
bastante antiguas de las librerías y en versiones más modernas, tanto
Slim como ReactPHP han modificado el API público
2. [reactive-slim]: parece una evolución de un usuario descontento del
proyecto anterior. Simplifica algunas cosas y completa alguna
funcionalidad. Bastante prometedora

Al final, la integración ha resultado ser más sencilla de lo esperado.

La aplicación crea un servidor HTTP implementado con ReactPHP 
([ejemplo en la documentación oficial][1]). 
Convierte la petición ReactPHP en una petición
Slim. Procesa la petición Slim, como cualquier otra API REST hecha
con dicha librería ([ejemplo en la documentación oficial][2]).
La respuesta Slim, la traduce a una respuesta
ReactPHP. Y es esa respuesta la que devuelve al cliente.

El código final es tan sencillo como lo siguiente:

```
<?php
require '../vendor/autoload.php';

use ...

$slimApp = (new RestApiBuilder())->build();
$middleware = new SlimBridgeMiddleware($slimApp);

$loop = React\EventLoop\Factory::create();
$socketServer = new React\Socket\Server(1337, $loop);
$httpServer = new \React\Http\Server($middleware);
$httpServer->listen($socketServer);

$loop->run();

// file: SlimBridgeMiddleware.php
class SlimBridgeMiddleware {
  //...

public function __invoke(ServerRequestInterface $request) {
    $slimRequest = $this->toSlimRequest($request);
    $response = $this->slimApp->process($slimRequest, new \Slim\Http\Response());
    return $this->toReactResponse($response);
  }

  protected function toSlimRequest(ServerRequestInterface $request) {
    return new \Slim\Http\Request(
      $request->getMethod(),
      $request->getUri(),
      new \Slim\Http\Headers($request->getHeaders()),
      \Slim\Http\Cookies::parseHeader($request->getHeader('Cookie')),
      [],
      $request->getBody(),
      []
    );
  }

  protected function toReactResponse(\Slim\Http\Response $response) {
    $statusCode = $response->getStatusCode();
    $headers = $response->getHeaders();
    $response->getBody()->rewind();

    return new \React\Http\Response(
      $statusCode,
      $headers,
      $response->getBody()->getContents()
    );
  }
}

```

`RestApiBuilder` construye una aplicación Slim cualquiera, como se puede ver
en cualquier ejemplo de la documentación oficial.

# Posibles puntos de mejora

Esta solución no es 100% completa, pero suficiente para los casos de
uso que tengo entre manos. Otros casos de uso podrían necesitar:

1. Peticiones parciales, o peticiones con gran cantidad de datos, como
algunas peticiones POST
2. Subir ficheros

## Referencias

- [Mis inicios con ZeroMQ][3]
- [Ejemplo de servidor HTTP implementado con ReactPHP][1]
- [Ejemplo de un API REST implementado con Slim][2]

[WebSocket]: https://es.wikipedia.org/wiki/WebSocket
[Slim]: http://www.slimframework.com
[ReactPHP]: https://reactphp.org
[reactphp-slim]: https://github.com/mbarquin/reactphp-slim
[reactive-slim]: https://github.com/NigelGreenway/reactive-slim/issues
[1]: https://reactphp.org/http/
[2]: http://www.slimframework.com/docs/v3/tutorial/first-app.html
[3]: https://rchavarria.github.io/notes/proyectos/aprendizaje/2018/04/24/zeromq-101.html
