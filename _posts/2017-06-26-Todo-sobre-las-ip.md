---
layout: post
title: Todo sobre las IP
category: Redes
comments: true
description: Una dirección IP es un número que identifica, de manera lógica y jerárquica a una interfaz de red de un dispositivo que utilice el protocolo TCP/IP. Este articulo se centra en las ips, los tipos de redes, y como hacer subredes.

tags:   
    - intro
    - protocolos
---

Según la wikipedia una ip es "Una dirección IP es un número que identifica, de manera lógica y jerárquica a una interfaz de red de un dispositivo que utilice el protocolo TCP/IP." En este articulo se centra en las ips, los tipos de redes y de como hacer subredes.

Una IP esta compuesta de cuatro octetos separadas por un punto, esto signfica que hay cuatro conjuntos de 8 bits, es decir, de 192.168.1.1, en verdad es 11000000 10101000 00000001 00000001.

## Máscara de red

Las máscaras de red es una combinación de bits que sirve para delimitar el ambito de una red de ordenadores. Por ejemplo con la ip de antes, la 192.168.1.1 su mascara de red seria 255.255.255.0 es decir, de la ip 192.168.1.1, los tres primeros octetos, serian 192.168.1, seran la para red y el cuarto octeto es para el host. En este caso la red seria 192.168.1.0 seria una mascara de 24 bits, o sea que la mascara tiene 24 numeros 1.

## Direcciones especiales

Hay ciertas IPs que no pueden ser usadas por un host, son estas:

* Direccion de red, toda la parte del host acabada en 0. por ejemplo 192.168.1.0
* Broadcast, para difundir mensajes a toda la red, es el ultimo host por ejemplo 255.255.255.255
* Localhost o Loopback, es la propia ip interna del host.

## Crear una subred

Por ejemplo queremos crear una subred dentro seria algo tan sencillo como usar una mascara de red de 25 bits, es decir nuestra mascara seria 255.255.255.128 esto haria que se separa la red en dos, una red con ips del 1 al 127 y otra red del 129 al 254.






