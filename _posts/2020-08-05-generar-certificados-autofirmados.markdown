---
layout: post
title: "Cómo generar certificados autofirmados"
date: 2020-08-05 11:11
author: Ruben Chavarria
categories: 
- Tutoriales
---

Este post trata sobre cómo podemos generar certificados SSL autofirmados en
Windows, con `mkcert`, para poder configurar servidores HTTPS.

El mérito no es mío, solamente he seguido los pasos detallados en un documento
elaborado por un compañero de trabajo.

<!-- more -->

El proceso a grandes rasgos es el siguiente:

- Crear un Autoridad de Certificación (CA)
- Registrar esa Autoridad de Certificación como una CA de confianza en el
almacén raíz de Windows y en tu navegador (si tu navegador no usa el almacén
de Windows)
- Crear un certificado SSL firmado por esta Autoridad de Certificación

## Instalar `mkcert`

Existen dos alternativas:

1. Seguir las [instrucciones oficiales]
2. Usar [Chocolatey]

Yo he ido por la segunda opción, porque es realmente fácil. Aunque, primero
habría que [instalar Chocolatey]. Cuidado con los requisitos de seguridad.
Yo no he tenido problemas instalándolo desde PowerShell con permisos de
administrador.

Para instalar `mkcert` con Chocolatey:

```
choco install mkcert
```

## Crear una Autoridad de Certificación

Abre un consola de PowerShell con permisos de administrador, y ejecuta el
siguiente comando:

```
mkcert -install
```

Se puede comprobar que se ha instalado correctamente si vamos a "Windows > 
Administrar certificados de usuario". En este diálogo de Windows deberíamos
encontrar la Autoridad de Certificación bajo el menú "Entidades de certificación
raíz de confianza > Certificados"

![Entidades de certificación raíz de confianza]({{ site.baseurl }}/assets/images/2020/mkcert-ca.png)

## Crear certificados firmados

Dentro de la consola PowerShell, ve al directorio donde quieres que se almacenen
los certificados y ejecuta:

```
mkcert tu.dominio.local
```

Donde `tu.dominio.local` será la dirección para acceder a tu servidor. Posiblemente
`mkcert localhost` te pueda servir.

Esta dirección debe existir en tu fichero de hosts, `C:\Windows\System32\drivers\etc\hosts`,
de lo contrario, el certificado se generará pero las peticiones al servidor no
llegarán correctamente.

Ese comando generará dos ficheros: `tu.dominio.local.pem` y `tu.dominio.local-key.pem`.
Son estos ficheros los que deberás usar para configurar tu servidor o aplicación.

El comando puede generar certificados para varios dominios, subdominios o direcciones
IP. Se pueden usar asteriscos, `*` (wildcards).

## Usar el certificado

A partir de aquí, es fácil encontrar guías para utilizar estos certificados en:
aplicaciones Node.js desarrolladas con Express, aplicaciones React creadas con
`create-react-app`, servidores Apache, Nginx,...

### Referencias

- [Herramienta `mkcert`]
- [Chocolatey], gestor de paquetes para Windows

[instrucciones oficiales]: https://github.com/FiloSottile/mkcert#installation
[instalar Chocolatey]: https://chocolatey.org/install
[Herramienta `mkcert`]: https://github.com/FiloSottile/mkcert
[Chocolatey]: https://chocolatey.org/
