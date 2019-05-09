---
layout: post
title: "Centralized logging with Elastic stack"
date: 2019-01-17 00:00
author: Ruben Chavarria
categories:
- Cursos
---

Notas tomadas sobre el curso [Centralized Logging with the Elastic Stack: Getting Started]
de [JP Toto] en [Pluralsight]. El curso muestra cómo usar y configurar
[Logstash], [Elasticsearch] y [Kibana] para centralizar y monitorizar
servidores, tráfico de red o aplicaciones.

<!-- more -->

## Introduction

Describe qué papel juega cada herramienta: Logstash, Elastic, Kibana y los
*Beats* (pequeños agentes instalados en cada máquina que queremos monitorizar)

## Configuring Elasticsearch

### Introducing the Monitoring Challenge

Comenzar desde el back (servidores) y moverse hacia adelante (interfaz de usuario)

Normalmente, el apartado de Elastic Search está compuesto de varios nodos (ver
curso [Administering an Elastic Search cluster]

La idea general es: hay múltiples *beats* instalados por toda nuestra red, cada uno
de ellos envía información a un servidor de Logstash. Éste, envía información
procesada a Elastic. Y esa información puede ser consultada y mostrada al
usuario con Kibana.

Los *beats* también pueden enviar datos directamente a Elastic. De hecho, parece
que los *beats* son mini-logstash, pueden filtrar y mejorar la información y
enviarla a distintos destinos.

### Installing Elasticsearch on Linux

Fácil, a través de paquetes. Elastic es instalado como un servicio de Linux

Se puede comprobar si está bien instalado con

```bash
$ curl http://localhost:9200
{
  "name": "your node name",
  "cluster_name": "your cluster name",
  ...
}
```

### Installing Elasticsearch on Windows Server

## Installing Logstash

### Introduction to Logstash

Logstash es un motor de colectar datos. Ingiere los datos (normalemente mensajes
de logs), los mejora o modifica y los envía hacía un sistema de almacenamiento.

Hay tres apartados que se pueden configurar:

1. `input`: de dónde van a venir los datos?
2. `filter`: tratamiento de los datos
3. `output`: dónde se van a almacenar?

### Installing Logstash

Se puede instalar desde paquetes `apt` en Ubuntu

Para comprobar que funciona, usar el comando:

```bash
$ <install-dir>/bin/logstash -e '\
  input { stdin {} } \
  output { \
    elasticsearch { hosts => [ "<elastic-ip" ] } \
  }'
```

El comando envía a nuestro servidor Elastic todo lo que escribamos en la consola
(`stdin`), no hay filtros configurados.

## Visualizing with Kibana

### Introduction to Kibana

### Installing and Configuring Kibana

Puede ser instalado a través de paquetes `apt` y también es instalado como un
servicio en Linux

## Instrumenting Windows Servers

### Installing and Configuring Winlogbeat

### Setting up Logstash for Beats

### Creating Winlogbeat Dashboards

Muestra cómo crear paneles de información en Kibana, comenzando por ir explorando
los datos almacenados en Elastic, creando visualizaciones (gráficos) y terminar
uniéndolos y organizándolos en dashboards o paneles

### Creating Metricbeat Dashboards

## Instrumenting Linux Servers

### Installing and Configuring Filebeat

### Creating Linux Dashboards

## Instrumenting Network Traffic

### Installing and Configuring Packetbeat on Windows

Nos permite identificar si hay picos de tráfico o mucho más tráfico de red de
lo normal.

Puede identificar tráfico dirigido a diferentes aplicaciones: MySQL,... Supongo
que simplemente mirando el puerto al que va dirigido.

### Graphing ICMP and HTTP Network Traffic in Kibana

## Instrumenting IIS Logs

### Configuring Filebeat and Logstash for IIS

### Graphing IIS Request Data with Kibana

## Alerting with Watcher

### Installing and Configuring Watcher

Watcher es un plugin comercial para Elasticsearch, no es gratis, aunque tienes
30 días de prueba. Es parte de la herramienta X-Pack

Watcher puede enviar alertas a muchos sitios diferentes: email, jira,...

Se debe instalar en cada nodo de Elasticsearch

### Setting up an Email Watch and Alert

Watcher funciona de la siguiente manera:

1. Se configura un trigger, algo que se ejecutará cada `X` tiempo
2. Lo que se ejecuta es una query, una petición a Elasticsearch
3. El resultado se compará con unos valores de referencia, para saber si se
cumple o no una condición determinada
4. Si la condición se cumple, se ejecuta una acción, por ejemplo, enviar una
alerta a algún sitio

## Referencias

- [Elastic guides], el primer sitio donde buscar por información y tutoriales

[Centralized Logging with the Elastic Stack: Getting Started]: https://app.pluralsight.com/library/courses/centralized-logging-elastic-stack
[JP Toto]: http://jptoto.jp/
[Pluralsight]: https://pluralsight.com/
[Logstash]: https://www.elastic.co/products/logstash
[Elasticsearch]: https://www.elastic.co/products/elasticsearch
[Kibana]: https://www.elastic.co/products/kibana
[Administering an Elastic Search cluster]: https://app.pluralsight.com/library/courses/administering-elasticsearch-cluster/
[Elastic guides]: https://www.elastic.co/guide/index.html
