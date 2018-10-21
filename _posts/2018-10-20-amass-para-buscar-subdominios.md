---
layout: post
title: Amass, la mejor aplicación para buscar subdominios
category: Hacking
comments: true
description: Amass, es una aplicación desarrollada en Go, que es la aplicación más rapida y efectiva para buscar subdominios, parte fundamental de la parte recon de una aplicación web. En este post aprenderas todo lo necesario para usar esta aplicación correctamente.
tags:   
    - recon
    - subdominio
---

Amass, es una aplicación desarrollada en Go, que es la aplicación más rapida y efectiva para buscar subdominios, parte fundamental de la parte recon de una aplicación web. En este post aprenderas todo lo necesario para usar esta aplicación correctamente.

<figure>
<img alt="Amass aplicación recomendada por @Jhaddix" class="img img-responsive" src="/resources/images/amass.jpg"/>
<figcaption>
Amass aplicación recomendada por @Jhaddix en su charla Bughunters methodology v3
</figcaption>
</figure>

## Instalar Amass

Esta aplicación funciona tanto para sistemas linux como para windows en windows, puedes descargarte la ultima versión de la aplicacion desde [aqui](https://github.com/OWASP/Amass/releases){:target="_blank"}.

En sistemas linux puedes descargarte la aplicación desde snap, buscando "amass".

<figure>
<img alt="Amass se puede descargar desde snap" class="img img-responsive" src="/resources/images/amass-en-snap.jpg"/>
<figcaption>
Amasss se puede descargar desde snap
</figcaption>
</figure>


## Usar Amass

Esta aplicación es de las más rapidas para buscar subdominios pero es una aplicación de consola, es decir no tiene interfaz grafica, es todo por comandos, para mi es un punto a favor.

### Comandos basicos

El primer paso más importante, saber donde esta la ayuda en Amass, es mediante -h, donde recibiremos todos los comandos disponibles.

{% highlight bash linenos %}

    amass -h

{% endhighlight %}

Empezando una busqueda de subdominios basica, con la opcion -d

{% highlight bash linenos %}

    amass -d facebook.com

{% endhighlight %}

donde recibiremos algo como esto:

{% highlight bash linenos %}

h1rd@dmz:~$ amass -d facebook.com
register.facebook.com
www.facebook.com
m.facebook.com
de.facebook.com
facebook.com
a.ns.facebook.com
edge-snaptu-http-mini-shv-01-amt2.facebook.com
edge-star-shv-01-mia3.facebook.com
edge-mqtt-shv-01-atl3.facebook.com
edge-z-m-mini-shv-01-iad3.facebook.com
edge-mqtt-shv-01-mia3.facebook.com
edge-star-shv-01-amt2.facebook.com
edge-z-m-mini-shv-01-atl3.facebook.com
edge-snaptu-http-p2-shv-01-sea1.facebook.com
secure-edge-latest-shv-01-mad1.facebook.com
cromwelledge-bgp-01-mad1.facebook.com
edge-atlas-shv-01-amt2.facebook.com
traceroute-bgp-01-sea1.facebook.com
edge-mqtt-mini-shv-01-mia3.facebook.com
edgeray-shv-01-sea1.facebook.com
edge-atlas-shv-01-iad3.facebook.com
edge-z-p3-shv-01-mia3.facebook.com
edge-z-p3-shv-01-sea1.facebook.com
edge-z-1-p2-shv-01-vie1.facebook.com
...

{% endhighlight %}

Extrayendo más datos, usando la opción -ip recibiremos la ip desde donde esta el subdominio alojado

{% highlight bash linenos %}

    amass -ip -d facebook.com

{% endhighlight %}

Y veremos los subdominios detectados con sus ips

{% highlight bash linenos %}
h1rd@dmz:~$ amass -ip -d facebook.com
work-98949980.facebook.com,179.60.192.3
work-94644431.facebook.com,179.60.192.3
mail2000.facebook.com,179.60.192.3
work-70529761.facebook.com,31.13.90.2
edge-snaptu-http-p2-shv-01-sea1.facebook.com,31.13.76.73
experiment-dns-science-300.facebook.com,66.220.152.19
m.0.facebook.com,31.13.90.37
0.facebook.com,31.13.90.37
...

{% endhighlight %}


## Comandos de fuerza bruta

En este apartado veremos varios comandos interesantes para buscar subdominios por fuerza bruta. Ten cuidado con estas operaciones ya que pueden sobrecargar tu red.

Comandos:

-brute despues de buscar subdominios ejecuta las operaciones de fuerza bruta
-min-for-recursive numero  esta operación habilita la posibilidad de volver a hacer fuerza bruta recursiva, es decir si pones -min-for-recursive 3 y en esta vuelta de fuerza bruta el programa solo encuentra 2 subdominios, no volvera a revisar a pasar
-norecursive esta opcion es para que el ataque de fuerza bruta solo sea sobre el dominio principal
-w nombrefichero cambias el diccionario de fuerza bruta que usara amass.



