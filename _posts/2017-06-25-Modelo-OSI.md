---
layout: post
title: Modelo OSI
category: Redes
comments: true
description: El modelo OSI, creado en 1980, es el modelo por referencia para los protocolos de la red, consiste en una normativa compuesta por siete capas que define las diferentes fases por las que deben pasar los datos para viajar de un dispositivo a otro en una red de comunicaciones.

tags:   
    - intro
    - protocolos
    - HTTP
---

El modelo OSI, creado en 1980, es el modelo por referencia para los protocolos de la red, consiste en una normativa compuesta por siete capas que define las diferentes fases por las que deben pasar los datos para viajar de un dispositivo a otro en una red de comunicaciones.

Este modelo esta compuesto por siete capas:

* Nivel fisico
* Nivel enlace de datos
* Nivel de red
* Nivel de transporte
* Nivel de sesión
* Nivel de presentación
* Nivel de aplicación

<figure>
<img alt="Modelo OSI" src="/resources/images/Modelo-osi.png"/>
<figcaption>
Representación grafica del modelo OSI
</figcaption>
</figure>

## Nivel fisico

Es la primera capa del modelo OSI, que se refiere a las transformaciones que se le hacen a la secuencia de bits para trasmitirlos de un lugar a otro.

## Nivel enlace de datos

El objetivo de esta capa es que la información fluya entre dos maquinas que esten conectadas directamente, para lograr este objetivo tiene que montar bloques de información o tambien llamadas tramas.

## Nivel de red

El objetivo de esta capa, es que los datos lleguen desde el origin al destino, incluso cuando estos no estan conectados directamente. Esto se hace mediante enroutadores. En esta capa se trabaja con paquetes. Y en esta capa es donde trabaja el protocolo IP.

## Nivel de transporte

El objetivo de esta capa es ocuparse del transporte de datos, de una maquina a otra, independientemente del tipo de red fisica que se use. En esta capa trabajan dos protocolos, TCP y UDP.
TCP es un protocolo orientado a la conexión, y trabaja con segmentos. Lo usamos cuando necesitamos todos los datos, por ejemplo al descargar una web.
UDP es un protocolo sin conexion, trabaja con datagramas, es bastante util cuando no es importante recibir todos los datos, por ejemplo una llamada VOIP.

## Nivel de sesión

Esta capa se encarga de mantener y controlar el enlace establecido entre dos computadoras que esten transmitiendo datos de cualquier tipo. En esta capa tendriamos los protocolos de HTTP y SSH.

## Nivel de presentación

En esta capa OSI, se encarga de representar la informacion, de manera que aunque distintos equipos puedan tener diferentes representaciones internas de caracteres (ANSI, Unicode..) los datos lleguen de manera reconocible, podria decirse que esta capa actua como traductor. 
Esta capa tambien permite cifrar los datos y comprimirlos.

## Nivel de aplicación

Esta capa, define los protocolos que utilizan las aplicaciones para intercambiar datos, como emails, navegadores, FTPs...


