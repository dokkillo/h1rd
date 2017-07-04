---
layout: post
title: Fase reconocimiento, comandos.
category: Hacking
comments: true
description: En otro articulo hablamos de como buscar informacion de la empresa mediante google hacking, webs, redes sociales. Ahora toca buscar informacion mediante comandos, como whois, ping, tracert, con los que podremos conocer más información sobre la empresa a auditar.

tags:   
    - hacker
    - pentesting

---

En otro articulo hablamos de como buscar informacion de la empresa mediante google hacking, webs, redes sociales. Ahora toca buscar informacion mediante comandos, como whois, ping, tracert.

## Whois

Este comando tanto de Windows como de Linux podremos sacar toda la información que haya sobre un dominio en particular, podremos encontrar emails, nombres de persona, direcciones, telefonos. A no ser que la empresa haya contratado para su dominio un servicio de coste anual que esconde esos datos publicos.

Tambien podemos acceder a ella en: [Whois](https://www.whois.com/whois/){:target="_blank"}

<div class="env-header">Comando whois</div>
{% highlight sql linenos %}

whois www.google.es

{% endhighlight %}

## Ping

Usando el comando ping al dominio web, podemos sacar la ip.

<div class="env-header">Comando ping</div>
{% highlight sql linenos %}

ping www.google.es

{% endhighlight %}

## Tracert 

__El comando tracert en windows, o traceroute en linux__ este comando nos ira diciendo los saltos que siguen nuestros datos hasta llegar al servidor, con ello podemos ver si pasa algun firewall etc.

<div class="env-header">Comando traceroute</div>
{% highlight sql linenos %}

traceroute www.google.es

{% endhighlight %}

## Consultas DNS

El comando nslookup (funciona tanto en windows como en linux) tiene un modo interactivo y un modo normal, es decir podemos escribir en nuestra consola nslookup y la ip o el nombre de dominio y recibir los datos o escribir nslookup y alli hacer todas las peticiones que queramos hacer y despues salir.

<div class="env-header">Comando nslookup</div>
{% highlight sql linenos %}

nslookup

{% endhighlight %}

En el modo interactivo podemos conocer por ejemplo, los servidores que se ocupan de gestionar los correos. Y al contrario que el comando Ping, podremos saber todas las ips asociadas a un dominio, no solo una.

<div class="env-header">Ver servidores de correos con nslookup</div>
{% highlight sql linenos %}

set type=mx
google.es

{% endhighlight %}



