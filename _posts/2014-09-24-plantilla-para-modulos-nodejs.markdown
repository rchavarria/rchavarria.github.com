---
title: "Plantilla para módulos NodeJS"
date: 2014-09-24 00:45
author: Rubén Chavarría
comments: true
categories: 
- JavaScript
- tutorial
- nodejs
published: true
footer: false
sidebar: true
---

Hace poco, viendo los [screencasts de Carlos Blé]
sobre programación, a un compañero de trabajo le picó la curiosidad e
intentó repetir el ejercicio que practicaba Carlos. Carlos desarrolla algunos
screencasts en JavaScript, y utiliza [Mocha] y [Chai] como frameworks para tests.
Yo recordé haber montado algo parecido algún día, y con este proyecto de github
quiero ayudar a los demás a que puedan montar un
[proyecto NodeJS con Gulp, Mocha y Chai].

<!-- more -->

# Plantilla para módulos NodeJS

En este proyecto encontrarás una estructura para módulos [NodeJS] lista
para comenzar a trabajar. El proyecto está compuesto de las siguientes
librerías:

- [Gulp]: como herramienta para automatizar tareas
- [Mocha]: como herramienta para ejecutar tests
- [Chai]: como librería de checkeos (*asserts* a falta de una traducción mejor)
para tests
- [Sinon]: como una librería de dobles de tests

En este fichero están las instrucciones para instalar y poner en funcionamiento
todas estas librerías.

# ¿Cómo instalar NodeJS?

Lo primero de todo, instalar NodeJS. 

Para instalarlo en Ubuntu, simplemente ejecutar el comando:

```bash
sudo apt-get install nodejs
```

Para instalarlo en otros sistemas operativos, visitarla página
[NodeJS download page].

Hay otra forma de instalarlo, y es a través de `nvm` ([Node Version Manager]).

El resto de librerías las instalaremos a través de la herramienta `npm`.

# Inicializar `npm`

Ejecutar el comando:

```bash
npm init
```

El comando te guiará por unos pasos para introducir información básica del módulo
donde trabajarás. Entre esa información se encuentra el nombre del proyecto,
la descripción y la version.

Un fichero `package.json` tipo podría ser el siguiente:

```json
{
    "name": "nodejs-module-template",
    "version": "0.0.0",
    "description": "A template for NodeJS modules",
    "main": "index.js",
    "directories": {
        "test": "test"
    },
    "dependencies": {},
    "devDependencies": {},
    "scripts": {
        "test": "test"
    },
    "author": "Ruben Chavarria http://rchavarria.github.io",
    "license": "BSD-2-Clause"
}
```

# Instalar Gulp

Es muy fácil, con `npm`:

```bash
npm install --save-dev gulp
```

El flag `--save-dev` insertará una nueva línea en el fichero `package.json` para
indicar a `npm` que hay una nueva dependencia para tiempo de desarrollo.

Para comprobar que se ha instalado correctamente, ejecutar el comando 
`gulp --version`.

# Configurar Gulp

Crea un fichero `gulpfile.js` en el directorio raiz del proyecto. El contenido
del fichero podría ser el siguiente:

```javascript
var gulp = require('gulp');

gulp.task('default', function() {
    console.log('Hello gulp!');
});
```

Ejecuta el comando `gulp` para ver un mensaje por consola.

# Instalar librerías de tests

Es tan fácil como instalar Gulp, simplemente escribir el comando:

```bash
npm install --save-dev mocha chai sinon sinon-chai
```

Para probar que se ha instalado Mocha adecuadamente, escribir
`node node_modules/mocha/bin/mocha --version`.

# Antes de escribir el primer test

Antes de escribir el primer test, crearemos un fichero de inicializacion para
Mocha, para inicializar las librerias y evitar tener que escribir el mismo 
código una y otra vez en todos nuestros tests.

Crea un fichero llamado `test/bootstrap.js` y escribe en él este contenido:

```javascript
global.chai = require('chai');
global.sinon = require('sinon');
global.expect = chai.expect;

var sinonChai = require('sinon-chai');
chai.use(sinonChai);
```

Esto cargará las librerías Chai y Sinon, crea una variable global llamada
`expect` (la usaremos en todos los tests) y configura Chai para que use métodos
y funcionalidades proporcionados por Sinon.

Ahora, crearemos una tarea en Gulp para ejecutar los tests. Para ello necesitamos
un plugin de Gulp que sea capaz de lanzar Mocha. Tan fácil como lo anterior:

```bash
npm install --save-dev gulp-mocha
```

Luego, edita el fichero `gulpfile.js` y déjalo como el siguiente:

```javascript
var gulp = require('gulp'),
    mocha = require('gulp-mocha');

gulp.task('test', function () {
    return gulp
        .src(['test/bootstrap.js', 'test/scripts/**/*.js'])
        .pipe(mocha({ reporter: 'spec' }));
});
```

# Ahora sí, el primer test

Crea un fichero llamado `test/scripts/firstSpec.js` con el siguiente contenido:

```javascript
describe('Mocha', function() {
    it('expects using Chai', function() {
        expect(2 + 2).equals(4);
    });
});
```

Para ejecutar este sencillo test, escribe el comando `gulp test`.

# Cómo escuchar cambios en ficheros de tests y de producción

Es posible configurar Gulp para ejecutar una tarea específica cada vez que un
fichero (o varios) cambia. Configuraremos que se ejecute la tarea `test` cada
vez que se cambie un fichero de test o de producción. Para ello, añade la 
siguiente tarea al fichero `gulpfile.js`.

```javascript
gulp.task('test-watch', function () {
    return gulp.watch(['src/scripts/**/*.js', 'test/scripts/**/*.js'], ['test']);
});
```

Para probar que funciona, escribe el comando `gulp test-watch`, cambia `firstSpec.js`
y guarda los cambios. Verás cómo el test se vuelve a ejecutar automáticamente.

# Por fin, probar algún código de producción

Escribe un sencillo módulo NodeJS que sume dos enteros, guárdalo como 
`src/scripts/adder.js`:

```javascript
module.exports = function adder(a, b) {
    return a + b;
};
```

Reemplaza el contenido de `test/scripts/firstSpec.js` por este otro (o escribe
tú mismo un nuevo fichero con este test):

```javascript
describe('Adder module', function() {
    // imports the adder module
    var adder = require('../../src/scripts/adder.js');

    it('adds two integers', function() {
        var sum = adder(2, 2);
        expect(sum).equals(4);
    });
});
```

Lánzalos con `gulp test`.

# Seguir leyendo

Puedes leer documentación de [Gulp] para saber cómo crear más y mejores tareas,
[Mocha] y [Mocha's plugin for Gulp] para conocer más sobre las opciones de Mocha,
[Chai] para aprender a escribir tests con el API `expect`, [Sinon] para aprender 
sobre dobles de tests (mocks, spies, stubs) cuando escribas tests.

# Actualización (05-07-2015)

He seguido ampliando este proyecto, y lo he adaptado para poder escribir código
ECMAScript 6: [Escribir y ejecutar tests de Mocha en ES6].

[screencasts de Carlos Blé]: http://www.carlosble.com/screencasts/es/
[proyecto NodeJS con Gulp, Mocha y Chai]: https://github.com/rchavarria/nodejs-module-template/tree/template-ready
[NodeJS]: http://nodejs.org
[Gulp]: http://gulpjs.com
[Mocha]: http://visionmedia.github.io/mocha/
[Mocha's plugin for Gulp]: https://github.com/sindresorhus/gulp-mocha
[Chai]: http://chaijs.com
[Sinon]: http://cjohansen.no/sinon
[NodeJS download page]: http://nodejs.org/download
[Node Version Manager]: http://carlosazaustre.es/blog/como-instalar-node-js-en-ubuntu
[Escribir y ejecutar tests de Mocha en ES6]: /blog/2015/07/05/escribir-tests-mocha-es6
