---
layout: post
title: Nmap mapeando la red
category: Hacking
comments: true
description: En este articulo hablaremos de dos partes fundamentales de NMAP, identificación de host y mapeo de la red. Mediante estas opciones podremos conocer nuestro objetivo más en profundidad. En esta fase lo más importante es que NMAP consiga una respuesta del host, da igual la respuesta, pero algo que demuestre que hay un host vivo detras de esa IP.
tags:   

    - pentesting
    - nmap

---

 En este articulo hablaremos de dos partes fundamentales de NMAP, identificación de host y mapeo de la red. Mediante estas opciones podremos conocer nuestro objetivo más en profundidad. En esta fase lo más importante es que NMAP consiga una respuesta del host, da igual la respuesta, pero algo que demuestre que hay un host vivo detras de esa IP. Esto lo conseguiremos creando paquetes modificados especialmente y analizando la respuesta que recibamos. 

Para la creacción de paquetes usaremos tres protocolos, Internet Control Message Protocol (ICMP), User Datagram Protocol (UDP) y Transmission Control Protocol (TCP)

## Internet Control Message Protocol (ICMP)

Este protocol se ocupa de pasar mensajes de un host a otro y de tareas de diagnostico de la red, NMAP usa este protocolo por ejemplo si enviamos una peticion de timestamp a un host este deberia respondernos. Lamentablemente para los exploradores de redes, muchos sistemas y cortafuegos ahora bloquean esos paquetes en lugar de responder como requiere el estándar RFC 1122. Por ésta razón los sondeos que sólo utilizan el protocolo ICMP no son muy fiables para analizar sistemas desconocidos en Internet.

Nmap tiene tres tipos de escaneos usando ICMP

__-PE__  Conocido como echo request o ping

__-PP__  Timestamp request, en esta opcion se le pide al host información sobre su time system, este contesta en formato decimal y en milisegundos desde la medianoche GMT, si el sistema devuelve la respuesta, NMAP sabe que esta online.

__-PM__ Subnet address mask request, esta opcion nos da la mascara de red usada por el host, si el sistema nos devuelve respuesta, Nmap nos informara que esta conectado.


## User Datagram Protocol (UDP)

UDP al contrario de TCP, es un protocolo no orientado a conexión, es decir cuando una maquina A envia paquetes a una maquina B, el flujo es unidireccional y la maquina B, no enviara confirmación de ningun tipo a la maquina A.

Al ser UDP no orientado a conexión, puede ser problematico deducir si ese sistema existe, pero hay dos opciones donde esto es posible:

* Que haya un servicio que siempre responda como DNS (es raro encontrarse con esto)
* Que el puerto cerrado (normal), por lo que recibiremos un mensaje ICMP de puerto no accesible, por lo que es recomendable cuando se hace un escan de UDP elegir un puesto que sepamos que estara cerrado, si no especificamos ningún puerto NMAP por defecto probara en el puerto 40125 -PU40125

Para hacer un escaner de UDP usaremos -PU


## Transmission Control Protocol (TCP)

Nmap tiene dos opciones para la identificacion de hosts usando paquetes TCP, -PS y -PA, ambas operan en el puerto 80 por defecto pero se pueden añadir otros puertos, listas etc.. en sistema unix es necesario ser root para ejecutar estos escaners.

__-PS o half open scanning__

Esta opción, NMAP empieza la comunicacion three-hand-shake con un SYN, como si fuera normal, el sistema responde como es normal con SYN,ACK y NMAP al ver que el sistema esta abierto, cierra la conexion con un RST.

__-PA__

En esta opción, NMAP, empieza la comunicación directamente con un ACK, como si ya existiera una comunicación anterior, por lo que el host enviara un paquete con RST pidiendo cerrar la comunicación y alli sabremos que hay un host en esa IP.


## Traceroute

traceoute es el comando con el que podemos saber todos los host por los que pasa un paquete entre la maquina A y la maquina B. para usarlo en NMAP es suficiente con --traceroute.






