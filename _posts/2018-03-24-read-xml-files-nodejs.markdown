---
layout: post
title: "Parsear ficheros XML con Node.js"
date: 2018-03-24 00:00
author: Ruben Chavarria
categories:
- Proyectos
- Node.js
- XML
---

Sí, todavía hay sistemas que utilizan XML como formato de salida de sus datos. En este caso, necesito poder parsear ficheros XML reportados por impresoras con información del nivel de tinta en sus cartuchos y otra información.
En principio, la idea que tengo es la de extraer dicha información mediante XPath, para no tener que recorrer el fichero nodo por nodo, hijos, y toda la estructura de árbol.

Todos los ficheros XML tendrán el mismo formato, por lo que con un solo parser podría extraer información de diversas máquinas.

En una primera búsqueda, parece que los paquetes `npm` [xpath] y [xmldom] son unas herramientas adecuadas para comenzar.

<!-- more -->

## Ejemplos básico

De la documentación oficial de la librería `xpath`...

Obtener directamente el valor de texto de un nodo:

```
var xml = "<book><title>Harry Potter</title></book>";
var doc = new dom().parseFromString(xml);
var title = xpath.select("string(//title)", doc);
 
console.log(title);
// resultado:
// Harry Potter
```

Los informes enviados por las impresoras utilizan *namespaces*, por lo que debo configuirar la librería para que los entienda. Un ejemplo de ello sería:

```
var xml = "<book xmlns:bookml='http://example.com/book'><bookml:title>Harry Potter</bookml:title></book>"
var select = xpath.useNamespaces({"bookml": "http://example.com/book"});
 
console.log(select('//bookml:title/text()', doc)[0].nodeValue);
// resultado:
// Harry Potter
```

Con esto, de un XML similar a:

```
<?xml version="1.0" encoding="UTF-8"?>
<xbpsdManagedInfo:xbpsdManagedInfo
  xmlns:xbpsdManagedInfo="http://schemas.brother.info/mfc/mailreports/"
  xmlns:bpsdm="http://schemas.brother.info/mfc/mailreports/1.00">
<bpsdm:NetInfo>
  <bpsdm:URL>http://xxx.18.xxx.41/general/status.html</bpsdm:URL>
  <bpsdm:FirmwareVersion>F</bpsdm:FirmwareVersion>
  <bpsdm:NodeName>BxN3x055xAB5x24</bpsdm:NodeName>
  <bpsdm:IPAddress Version="4">xxx.18.xxx.41</bpsdm:IPAddress>
  <bpsdm:MACAddress>30:05:5c:ab:55:24</bpsdm:MACAddress>
  <bpsdm:Location></bpsdm:Location>
  <bpsdm:Contact></bpsdm:Contact>
</bpsdm:NetInfo>
<bpsdm:DeviceInfo>
  <bpsdm:ModelName></bpsdm:ModelName>
  <bpsdm:SerialNumber>E75337M5N131720</bpsdm:SerialNumber>
  <bpsdm:PrinterFirmware>5.19</bpsdm:PrinterFirmware>
  <bpsdm:PrinterFirmware Category="Sub">1.02</bpsdm:PrinterFirmware>
  <bpsdm:MemorySize Unit="Mbytes">256</bpsdm:MemorySize>
</bpsdm:DeviceInfo>
...
```

Puedo extraer el número de serie con un código ocmo éste:

```
const xml = // read xml report
const doc = new dom().parseFromString(xml);
const select = xpath.useNamespaces({
  'bpsdm': 'http://schemas.brother.info/mfc/mailreports/1.00'
});

const sn = select('string(//bpsdm:SerialNumber)', doc);
console.log('Serial Number:', sn);
// imprime:
// E75337M5N131720
```

A partir de aquí, ya puedo organizar mi código para que vaya extrayendo toda la información que necesito.

## Errores encontrados

Bueno, a parte de un par de errores por no saber ni siquiera copiar los ejemplos de `xpath`, que no voy a poner aquí por no ser interesantes, me he encontrado con:

```
/home/rchavarria/projects/brthr-email-reader/node_modules/xpath/xpath.js:2311
        throw new Error("Cannot resolve QName " + prefix);
        ^

Error: Cannot resolve QName bpsdm
    at Function.NodeTest.nameSpaceMatches (/home/rchavarria/projects/brthr-email-reader/node_modules/xpath/xpath.js:2311:15)
    at Object.matches (/home/rchavarria/projects/brthr-email-reader/node_modules/xpath/xpath.js:2337:16)
    at Function.PathExpr.applyStep (/home/rchavarria/projects/brthr-email-reader/node_modules/xpath/xpath.js:1865:26)
    at /home/rchavarria/projects/brthr-email-reader/node_mo
```

> No se puede resolver el QName bpsdm

¡Qué casualidad! `bpsdm` coincide con el namespace utilizado en el fichero XML. De este error supuse que debía configurar `xpath` para que usase namespaces. Fue fácil y directo.




