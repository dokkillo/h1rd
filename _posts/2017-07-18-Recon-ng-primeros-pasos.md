---
layout: post
title: Primeros pasos con Recon-ng
category: Hacking
comments: true
description: En la fase de reconocimiento, es necesario conseguir toda la información posible sobre nuestro objetivo, una de las maneras es mediante OSINT o Open Source INTeligence, es decir, recolección de información mediante fuentes abiertas y gratuitas de internet. Es aqui donde entra Recon-ng, un framework de reconocimiento web, escrito en python.

tags:   
    - hacker
    - pentesting
    - recon-ng

---

En la fase de reconocimiento, es necesario conseguir toda la información posible sobre nuestro objetivo, una de las maneras es mediante OSINT o Open Source INTeligence, es decir, recolección de información mediante fuentes abiertas y gratuitas de internet. Es aqui donde entra Recon-ng, un framework de reconocimiento web, escrito en python.

Recon-ng esta compuesto de modulos, hay 90 de ellos, tienen diferentes funciones, desde Reporting, Recon, discovery...

Al ser una aplicación de linea de comandos, hay ciertos comandos que nos ayudaran al principio para navegar en la aplicación:

* help aqui encontraremos varios comandos basicos y que hacen

* show modules listado de mRecon-ngodulos de recon-ng, si queremos ver o usar alguno de estos modulos, tenemos que escribir use y el nombre del modulo, y dentro ya podremos escribir show info. Para salir de la sección de modulos y volver atras, Ctrl + C o escribir back.
Los whois con dominios .es dan problemas.

{% highlight sql linenos %}

[recon-ng][default] > use whois_pocs
[recon-ng][default] > show info

{% endhighlight %}

* show tables listado de tablas donde recon-ng guarda informacion, si por ejemplo luego escribimos show credentials nos mostrara todas las credenciales que hemos ido guardando en la base de datos interna de recon-ng


## Proceso de instalación

Recon-ng es una aplicación para Linux, no es [compatible con Windows](https://bitbucket.org/LaNMaSteR53/recon-ng/issues/205/recon-ng-in-windows-10){:target="_blank"}, viene instalada por defecto en Kali.

En Ubuntu o Mint se puede instalar con un apt-get install recon-ng, pero en otros sistemas como puede ser debian, no es posible, alli habria que bajar las fuentes que estan en la [web oficial del proyecto](https://bitbucket.org/LaNMaSteR53/recon-ng/src){:target="_blank"} y ejecutarlas, es necesario Python 2.7. No funcionan con Python 3.

Cuando lo ejecutemos saldra una lista de errores en rojo, no es ningún fallo, falta que pongamos las API de la redes sociales que usaremos para hacer OSINT,lo haremos más adelante.

## Trabajando con diferentes proyectos

Recon-ng permite trabajar con diferentes proyectos a la vez, asi mantener los datos de los targets que vamos recopilando información de una manera separada y organizada.

Para crear un nuevo proyecto, esto nos generara una base de datos diferente donde podremos gestionar los datos del nuevo target:

{% highlight sql linenos %}

[recon-ng][default] > workspaces add nombreproyecto

{% endhighlight %}

Para movernos entre los proyectos:

{% highlight sql linenos %}

[recon-ng][default] > workspaces select nombreproyecto

{% endhighlight %}

Para ver todos los proyectos:

{% highlight sql linenos %}

[recon-ng][default] > show workspaces

{% endhighlight %}

## Añadiendo datos...

Es momento de empezar añadiendo datos de nuestro target, esto lo haremos de la siguiente manera:

* Para añadir dominios web, escribiendo "add domains" con esto, nos ira preguntando los datos que necesita.

{% highlight sql linenos %}

[recon-ng][default] > add domains

{% endhighlight %}

* Dentro de cada dominio, puede haber varios subdominios, estos se almacenan en la tabla hosts, para ello o los ponemos a mano:

{% highlight sql linenos %}

[recon-ng][default] > add hosts

{% endhighlight %}

o usamos el modulo el modulo google_site_web, ello nos añadira todos los subdominios que encuentre.

* Para añadir compañias, escribimos "add companies". Donde añadiremos el nombre real de la compañia a buscar.

{% highlight sql linenos %}

[recon-ng][default] > add companies

{% endhighlight %}


En el siguiente post seguire profundizando en Recon-ng, donde ya pondremos las keys de redes sociales y podremos buscar más info.





