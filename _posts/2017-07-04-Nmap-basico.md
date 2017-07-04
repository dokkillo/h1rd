---
layout: post
title: Nmap basico
category: Hacking
comments: true
description: Nmap (Network mapper) es un scanner de seguridad usado para descubrir hosts y servicios en una red ayudandonos a crear un mapa detallado de toda la red. Nmap es un programa de codigo abierto creado por Gordon Lyon para Linux, pero actualmente el desarrollo esta a cargo de la comunidad y es multiplataforma.

tags:   
    - hacker
    - pentesting
    - nmap

---

Nmap (Network mapper) es un scanner de seguridad usado para descubrir hosts y servicios en una red ayudandonos a crear un mapa detallado de toda la red. Nmap es un programa de codigo abierto creado por Gordon Lyon para Linux, pero actualmente el desarrollo esta a cargo de la comunidad y es multiplataforma.
Puede descargarse en: [Nmap](https://nmap.org/){:target="_blank"}


Funciones:

* Descubrimiento de host
* Identificacion de puertos abiertos de una maquina objetivo
* Determina que servicios estan ejecutandose en la misma
* Identificación de que SO y version que usa la maquina objetivo
* Identificacion de algunas caracteristicas del hardware de la red
* Ampliacion de funciones mediante scripts.

Aunque es una aplicación de consola, tambien hay una version con GUI, Zenmap, puedes descargarla en [Zenmap](https://nmap.org/zenmap/){:target="_blank"}

## Usos basicos

El uso más simple de Nmap es usarlo de la siguiente manera:

{% highlight sql linenos %}

nmap 192.168.0.1

{% endhighlight %}

Aunque para pasar targets, tenemos más opciones, como las siguientes:

* Podriamos pasar la url

{% highlight sql linenos %}

nmap google.es

{% endhighlight %}

* Una lista, que en este caso nos escanearia 192.168.54.1, 192.168.54.10, 192.168.55.1, 192.168.55.10

{% highlight sql linenos %}

nmap 192.168.54,55.1,10

{% endhighlight %}

* Un rango en este caso el scan ira de 192.168.64.20 a 192.168.64.29

{% highlight sql linenos %}

nmap 192.168.64.20-29

{% endhighlight %}

* CIDR, rango de red por ejemplo en este caso el scan ira de 192.168.128.240 a 192.168.128.247

{% highlight sql linenos %}

nmap 192.168.128.240/29

{% endhighlight %}

__Si tienes dudas o quiere comprobar que lo que vas a scanear es realmente lo que has puesto, ante del scanner puedes usar -sL y te dira que maquinas vas a scanear.__


## Puertos

Para escanear directamente sobre un puerto es con el comando -p, el rango de puertos funciona igual que el rango de host a escanear, pero en este caso tambien podemos filtrar por tipo de protocolo, por ejemplo para escanear el puerto UDP 25 y el TCP 80 seria asi:

{% highlight sql linenos %}

nmap -p U:25,T:80 192.168.128.1

{% endhighlight %}


## Servicios

Nmap internamente trabaja con un fichero con más de 20000 puertos asociados a ficheros, donde es posible escanear los puertos en busca del servicio directamente, por ejemplo, si quisieramos saber si una maquina tiene el puerto de vnc abierto, pondriamos esto:

{% highlight sql linenos %}

nmap -p vnc 192.168.128.1

{% endhighlight %}

Si quisieramos saber si la maquina en cuestion tiene algun servicio relacionado con http abierto, seria con una wildcard asi:

{% highlight sql linenos %}

nmap -p http* 192.168.128.1

{% endhighlight %}





