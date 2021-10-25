---
layout: post
title: "Apache Kafka explained"
date: 2021-10-25 17:00
author: Ruben Chavarria
categories:
- Video
- Herramientas
---

Aquí están las notas tomadas del vídeo [Apache Kafka explained], donde se explican
los conceptos fundamentales de la herramienta [Apache Kafka].

<iframe width="560" height="315" src="https://www.youtube.com/embed/JalUUBKdcA0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<!-- more -->

### Kafka

A menudo, [Apache Kafka] se define como un **log de eventos distribuído**, donde
los mensajes son inmutables, y los nuevos mensajes se añaden al final de la
cola de mensajes

Los mensajes son guardados en disco, durante un cierto período de tiempo
(configurable supongo) llamado *retention policy*

Esta persistencia hace que Kafka sea una mezcla de sistema de mensajería y 
base de datos

### Pub/Sub (publicar/suscribir)

Es un método de envío de mensajes, donde quien publica los mensajes no sabe quién
o quienes están escuchando. De hecho, ni siquiera es necesario que haya nadie
escuchando

Quien escucha, tampoco necesita saber qué o quién está publicando mensajes

En este método, suele haber una tercera parte involucrada, el *broker*

A menudo se compara este patrón con un *tablón de anuncios* (bulletin board)

### Broker

Tercer elemento en el patrón pub/sub

Aísla al emisor del mensaje (publisher) del receptor o receptores del mismo
(subscriber), permitiendo una gran flexibilidad de organización y reduciendo
también el número de conexiones entre ellos, ya que se eliminan las conexiones
punto a punto entre todos los emisores y todos los receptores

### Usos de Kafka

1. Flujos de datos en tiempo real
2. *Tuberías* de datos: traspaso de datos de un sistema a otro
3. Lugar centralizado de almacenamiento y distribución de eventos
4. ETL, del inglés: extract, transform, load
5. CDC, change data capture
6. Big data ingest

### Arquitectura

Un típico sistema en Kafka consiste de varios *productores* (que publican mensajes
para un determinado *tópico*), varios *consumidores* (que consumer esos mensajes)
y de un *cluster*

Un cluster consiste en varios (típicamente 3) brokers. Su función es asignar
*offsets* y guardar los mensajes en disco

### Tópicos

Los mensajes publicados se envían a un determinado *topic*

Los topics son una forma de organizar y categorizar los datos, y se pueden dividir
en *particiones*

Cada partición tiene su propio *commit log* (como una copia inmutable de los mensajes)
y un orden garantizado de entrega

Cada consumidor, puede consumir de particiones diferentes, haciendo que sea muy
fácil escalar y permitiendo un alto rendimiento en la entrega de mensajes (throughput)

### Mensajes

Es la unidad de dato que se puede enviar o recibir

Para Kafka, es solo un array de bytes

Cada mensaje puede ser escrito en particiones diferentes dentro del mismo tópico,
típicamente round-robin. Por lo que si queremos un cierto orden, el productor
debe seleccionar qué partición escribir

Los mensajes pueden ser enviados en lotes (batches)

El orden de entrega no está garantizado entre particiones. La única forma de 
garantizar algún orden es el de tener una sola partición

Cada partición puede estar almacenada en distintos servidores, lo que permite que
un único topic pueda escalar horizontalmente

### Consumidores

Los consumidores leen mensajes del cluster. Para ello, se suscriben a uno o varios
topics. Los mensajes los reciben en el mismo orden que fueron producidos

Cada consumidor guarda un *offset* para saber qué mensaje fue el último que
consumió

Cada offset corresponde a un determinado mensaje en una determinada partición

Estos offsets pueden ser almacenados en Kafka (o Zookeeper) para poder parar y
arrancar de forma fácil

Cada consumidor pertenece a un *grupo de consumidores* (consumer group)

Los topics son consumidos por cada consumer group. Cada partición cuida que solo
un consumidor dentro de un consumer group esté consumiendo mensajes. Esto permite
escalar los consumidores de forma horizontal (cada consumidor consumirá de una
partición diferente del topic)

Si queremos consumir un mensaje varias veces, deberemos hacerlo en grupos diferentes

### Cluster

Un cluster está formado por varios brokers

Uno de ellos actúa como *cluster controller*, con las siguientes funciones

1. Asignar particiones a brokers (un topic puede tener particiones en distintos
brokers)
2. Monitoriza errores en los brokers
3. Uno de los brokers será elegido como *partition leader*, una forma de distribuir
el funcionamiento de las particiones
4. Productores y consumidores deben conectarse con el líder de la partición

### Retention

Una de las claves de Kafka es su almacenamiento de mensajes

Kafka almacena los mensajes:

1. Durante un período de tiempo: típicamente 7 días
2. Hasta un determinado tamaño del topic

Los mensajes más viejos, se eliminan

Se puede configurar por tópico

### Fiabilidad (*Reliability guarantees*)

Se garantiza el orden de entrega de los mensajes dentro de una partición de un
tópico

Un mensaje se considera *committed* cuando se ha escrito en el líder y se ha sincronizado
con todas sus réplicas. Estos mensajes no se pierden mientras exista una réplica
viva y se mantenga la *retention policy*

Los consumidores solo pueden leer este tipo de mensajes

La semántica de entrega de Kafka es: *al menos uno*, para garantizar la entrega
de mensajes

La semántica que no utiliza es *exactamente uno*, por lo que el mismo mensaje
puede ser entregado más de una vez. De esta forma, debemos apoyarnos en un sistema
externo de generación de claves (para identificar *duplicados*) o usar los
nuevos *Kafka streams*

### Trade-offs, encontrar un balance entre dos opciones

Debemos elegir entre fiabilidad y consistencia frente a disponibilidad, alto
rendimiento y baja latencia

Pros:

- Ayuda a reducir la complejidad de integración de distintos sistemas
- Permite varios productores y varios consumidores
- Persistencia en disco
- Alto rendimiento (troughput)
- Fácilemente escalable
- Tolerante a fallos

Cons:

- Se necesita mucho tiempo para comprender su complejidad y no dispararte en el pie
- Puede que no sea la mejor solución para sistemas que realmente necesiten una
baja latencia

¿Cuáles son las diferencias entre JMS (RabbitMQ, ActiveMQ) y Kafka?

En Kafka, son los consumidores los que hacen la petición para recibir mensajes
(consumers *pull* messages from brokers). Mientras que en JMS los mensajes son
entregados a los consumidores (messages are *pushed* to consumers)

En Kafka es muy fácil comenzar a recibir mensajes desde el principio del log

[Apache Kafka explained]: https://www.youtube.com/watch?v=JalUUBKdcA0
[Apache Kafka]: https://kafka.apache.org/
