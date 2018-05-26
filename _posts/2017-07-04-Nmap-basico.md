---
layout: post
title: Nmap basico
category: Hacking
comments: true
description: Nmap (Network mapper) es un scanner de seguridad usado para descubrir hosts y servicios en una red ayudandonos a crear un mapa detallado de toda la red. Nmap es un programa de codigo abierto creado por Gordon Lyon para Linux, pero actualmente el desarrollo esta a cargo de la comunidad y es multiplataforma.

tags:   


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

Otra opcion, es buscar en la maquina los puertos abiertos más frecuentes, ya que NMAP guarda junto con cada puerto un contador con los más frecuentes, si quisieramos buscar los 5 puertos abiertos más frecuentes, en este caso la consulta seria:

{% highlight sql linenos %}

nmap --top-ports 5 192.168.128.1

{% endhighlight %}

__Si a Nmap no se pone algun puerto, el por defecto busca los 1000 puertos más usados, --top-ports 1000__

Otro comando muy interesante a usar, es --reason con esta opción cada puerto nos dira el motivo del porque nmap a decidido, si esta open, closed, o filtered. Y con eso nosotros podremos decidir si es un falso negativo o no.

{% highlight sql linenos %}

nmap --top-ports 5 --reason 192.168.128.1

{% endhighlight %}


## Exportar datos

Cuando hacemos un escaneo, nos interesa guardarlo en un fichero para luego mostrarlo en el reporte final, esto lo podemos hacer con la opcion -o que además tiene varios modificadores, como por ejemplo, N que pondra todo exactamente igual que hemos visto en pantalla, o X que lo guardara en formato XML o G que escribe todo en una linea asi facilita la separacion a posteriori con el comando grep.


{% highlight sql linenos %}

nmap -oN reporte.txt --top-ports 5 --reason 192.168.128.1

{% endhighlight %}








