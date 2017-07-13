---
layout: post
title: Nmap evadiendo firewalls
category: Hacking
comments: true
description: En el mundo empresarial real, los equipos estan protegidos detrás de firewalls, IDS o NATs. En este post hablaremos de las diferentes maneras que usa NMAP para saltarse esas defensas y seguir haciendo su trabajo.

tags:   
    - hacker
    - pentesting
    - nmap
    - firewall
    - ids

---

En el mundo empresarial real, los equipos estan protegidos detrás de firewalls, NAT, IDS u otras defensas. En este post hablaremos de las diferentes maneras que usa NMAP para saltarse esas defensas y seguir haciendo su trabajo.
Las defensas más habituales que nos encontraremos seran:

* Firewalls
* NAT
* IDS

## Firewalls

Un firewall es un sistema de seguridad que controla el trafico de red que pasa entre dos redes, se ocupa de mirar los paquetes que viajan de una red a otra, permitiendo o denegando basandos en la cabecera del paquete o a veces el contenido de este. Toma las decisiones principalmente basandose en el socket (ip y puerto) y tambien según los flags activos.

Hay tres tipos de firewalls principales:

* Stateless, este firewall se basa en unas reglas, si el paquete a entrar cumple esas reglas, por ejemplo acceso al puerto 80, se le deja pasar, sino no. No inspecciona los flags de los paquetes TCP.
* Statefull, este tipo de firewall se basa en una serie de reglas añadidas por el administrador como el firewall tipo stateless, pero tambien se basa según el estado de la conexion, es decir mantienen una tabla con las conexiones aceptadas y establecidas, por lo que si llega un paquete que no es una conexion establecida con un flag RST o un paquete con NFX, este paquete sera eliminado.
* Proxy, este tipo de firewall se ocupa de interpretar el contenido del paquete y permitirlo o no según sus reglas, si el paquete  es de un contenido que no soporta, el firewall se comporta como si fuera un statefull firewall.


## Como saber que hemos encontrado un firewall

Hay tres opciones que podemos usar con NMAP para deducir que hemos encontrado un firewall, estas son __-traceroute__, __-O__ y __--badsum__ esta opción hace que NMAP cree un checksum incorrecto en la cabecera de TCP, todos los hosts borraran los paquetes, y si hubiese alguna respuesta, esta vendria de un firewall.
Más sobre esta tecnica en [Nmap bad cheksum](https://nmap.org/p60-12.html){:target="_blank"} 

## Maneras para saltarse un firewall



