---
layout: post
title: Nmap escaneo de puertos
category: Hacking
comments: true
description: El escaneo de puertos es la funcionalidad principal y la razón por la que se creo NMAP, en otros articulos hemos hablado de como escanear puertos, pero aqui hablaremos de las opciones de como decirle a NMAP que escanee esos puertos. Con la lista de host activos que hemos conseguido de la fase de enumeración, ahora necesitamos averiguar que función hace cada host, ¿es un web server?  ¿tiene la base de datos?

tags:   


    - nmap

---

 El escaneo de puertos es la funcionalidad principal y la razón por la que se creo NMAP, en otros articulos hemos hablado de como escanear puertos, pero aqui hablaremos de las opciones de como decirle a NMAP que escanee esos puertos. Con la lista de host activos que hemos conseguido de la fase de enumeración, ahora necesitamos averiguar que función hace cada host, ¿es un web server?  ¿tiene la base de datos?


## Tipos de escaneos de puerto

En NMAP para habilitiar un escaneo de puertos se crea mendiante una s minuscula y la letra del escan en mayuscula. En este articulo hablaremos de siete de estos tipos de escan. Hay varios más, puedes verlos en la [Pagina oficial de NMAP](https://nmap.org/book/man-port-scanning-techniques.html){:target="_blank"}.

## Resultado del escaneo de puertos

Al ejecutar un escaneo de puertos con nmap podemos recibir varios resultados:

* Open, el puerto esta abierto
* Closed, el puerto esta cerrado
* Filtered, el puerto esta prohibido o esta filtrado
* Sin respuesta.


## -sU Escaneo UDP

{% highlight sql linenos %}

nmap -sU 192.168.1.1

{% endhighlight %}

como hemos comentado en varios articulos, UDP es un protocolo no orientado a conexión por lo que no recibir respuesta no signfica que el puerto este cerrado, en este escan pueden ser diferentes cosas dependiendo del resultado.

* Los puertos abiertos en UDP son facilmente detectables cuando devuelven una respuesta, por ejemplo DNS o SNMP, pero otros servicios no devuelven ninguna respuesta.

* Los puertos cerrados, devuelven una respuesta de puerto inaccesible.

* Puertos filtrados, aqui podria estar filtrado por el router no dejandonos acceder al host por ese puerto, pero en el host tener ese puerto cerrado, o abierto.

* Sin respuesta, aqui tambien nos podemos encontrar o que el router bloquea nuestros paquetes y no nos devuelve respuestas, o el puerto esta abierto y al ser UDP no devuelve tampoco respuestas.

## -sT Connect Scan

{% highlight sql linenos %}

nmap -sT 192.168.1.1

{% endhighlight %}

Este es un escan TCP, consiste en realizar un "three way handshake" completo al puerto elegido. Dependiendo de la respuesta tenemos varias opciones:

* Puertos abiertos, hemos recibido la respuesta correcta.

* Puertos cerrados, devuelven un RST de puerto inaccesible.

* Puerto filtado o sin respuesta, el puerto esta filtrado por el router bloqueando la respuesta.


## -sS Half Scan

{% highlight sql linenos %}

nmap -sS 192.168.1.1

{% endhighlight %}

Por cada puerto NMAP comienza un "three way handshake" pero al recibir respuesta del host, cierra la conexion con un RST. Para realizar este scan es necesario tener permisos como administrador o root. Este es el scan más rapido y que menos recursos gasta tanto para el sistema como para el host.

* Puertos abiertos, hemos recibido la respuesta correcta.

* Puertos cerrados, devuelven un RST de puerto inaccesible.

* Puerto filtado o sin respuesta, el puerto esta filtrado por el router bloqueando la respuesta.


## -sN, -sF, -sX  Null, Fin y XMAS scan

{% highlight sql linenos %}

nmap -sN 192.168.1.1
nmap -sF 192.168.1.1
nmap -sX 192.168.1.1


{% endhighlight %}

Estos tres scan se basan en modificar los flags del paquete TCP, el scan null no añade nigún flag, el scan Fin, añade el flag FIN, y el scan XMAS, añade los flag: URG, PSH y FIN, haciendo que el paquete parezca un arbol de navidad (de alli su nombre...), lo importante es que los flags de SYN, ACK y RST no esten activos.

* Puertos abiertos, al ser paquetes con formato incorrectos, estos paquetes seran desechados y nunca recibiremos respuesta.

* Puertos cerrados, devuelven un RST de puerto inaccesible.

* Puerto filtado o sin respuesta, el puerto esta filtrado por el router bloqueando la respuesta.

Al no recibir respuesta clara si un puerto esta abierto o no, estos scan pierden mucho su utilidad,pero pueden ser utiles en caso donde haya firewalls o para evitar la detección de un IDS. Deben ser usados como ultimo recurso.

## -sA ACK scan

{% highlight sql linenos %}

nmap -sA 192.168.1.1

{% endhighlight %}

Este scan consiste en enviar un ACK al puerto del host.

* Puertos abiertos, Puertos cerrados, devuelven un RST en ambos casos ya que o el puerto puede ser inaccesible o para decirnos que la comunicación es incorrecta.

* Puerto filtado o sin respuesta, el puerto esta filtrado por el router bloqueando la respuesta.

Esta opción es muy buena para mapear las reglas del firewall, ya que si recibimos un RST es que el firewall nos dejo pasar, si no, es que el firewall nos cerro el paso.








