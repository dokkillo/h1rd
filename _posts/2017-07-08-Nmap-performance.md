---
layout: post
title: Nmap performance
category: Hacking
comments: true
description: En NMAP no hay ningún problema cuando en el primer scan nos devuelve que el puerto esta abierto o cerrado, perfecto, el problema esta cuando el sistema no lo sabe o no esta seguro, alli NMAP seguira intentandolo, pero el problema ¿hasta cuando?, ¿cuantas veces? puede que no nos interese congestionar la red, o llamar mucho la atención, o si la red esta muy congestionada en ese momento, nos vale la pena esperar un poco. En este articulo hablaremos de diferentes maneras para poder gestionar el tiempo y el performance de nuestros escaneos.

tags:   

    - pentesting
    - nmap

---

En NMAP no hay ningún problema cuando en el primer scan nos devuelve que el puerto esta abierto o cerrado, perfecto, el problema esta cuando el sistema no lo sabe o no esta seguro, alli NMAP seguira intentandolo, pero el problema ¿hasta cuando?, ¿cuantas veces? puede que no nos interese congestionar la red, o llamar mucho la atención, o si la red esta muy congestionada en ese momento, nos vale la pena esperar un poco. En este articulo hablaremos de diferentes maneras para poder gestionar el tiempo y el performance de nuestros escaneos.

En algunos de los siguientes comandos de los que hablaremos, seran para añadir un tiempo determinado, en nmap podemos añadir o milisegundos (ms), segundos (s), minutos (m) u horas (h), por defecto si no añadimos nada, seran en segundos.

{% highlight sql linenos %}

nmap --host-timeout 2m 192.168.1.1
nmap --host-timeout 24h 192.168.1.1

{% endhighlight %}

## Opciones para performance


* --max-retries con esta opcion especificamos el numero maximo de intentos antes de darnos por vencidos.
* --initial-rtt-timeout cuando empezamos a escanear un sistema, no sabemos este donde se encuentra, si en la habitación de al lado o en otro continente, por lo que se puede añadir un valor de espera de timeout antes de volver a intentarlo. Si el objetivo contesta, se ajusta el tiempo de espera correctamente.

{% highlight sql linenos %}

nmap --initial-rtt-timeout 3s 192.168.1.1

{% endhighlight %}

* --min-rtt-timeout, --max-rtt-timeout podemos añadir un maximo y un minimo para el timeout 
* --scan-delay --max-scan-delay con estas opciones podemos pausar NMAP entre intento e intento.
* --min-hostgroup --max-hostgroup nmpa testea por grupos, con estas opciones podemos controlar el tamaño del grupo a testear.
* --min-parallelism --max-parallelism con esto controlamos los escaners en paralelo que se estan ejecutando a la vez.
* --min-rate --max-rate con esto controlamos los scaners que enviamos por segundo.

## Plantillas de performance

Todas las opciones de antes, las controla NMAP internamente para su autogobierno centrandose siempre en la fiabilidad de los resultados que dara, aun asi hay plantillas donde ya nos define esos campos según la potencia que queramos darle a NMAP, funciona con -T y un numero, a numero más alto más potencia. 
Si no podemos ninguna opcion, por defecto siempre coge T3.
En la tabla podeis haceros una idea de lo que hace cada plantilla.


{% highlight sql linenos %}

nmap -T 4 192.168.1.1
nmap -T polite 192.168.1.1

{% endhighlight %}


<figure>
<img alt="Tabla de las plantillas de NMAP" src="/resources/images/nmap-templates.jpg"/>
<figcaption>
Tabla de las plantillas de NMAP. 
</figcaption>
</figure>
