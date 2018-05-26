---
layout: post
title: ¿Que es el SQL Injection?
category: Hacking
comments: true
description: SQL Injection es la primera vulnerabilidad que buscara cualquier hacker en una pagina web. Es un ataque facil de hacer, y cuyo resultado puede ser catastrofico para una empresa.
tags:
    - injection
    - owasp

---


SQL injection o inyeccion de SQL es una vulnerabilidad donde el atacante puede modificar una query correcta y cambiar asi el funcionamiento de la web. Puede haber inyecciones de otros tipos como (LDAP, XPath, nosql, os....) pero en este articulo me centrare en SQL. Es un ataque muy simple de realizar, en el que solo hay que modificar la url del navegador, y lo peor, que puede llevar a perder o que modifiquen toda la informacion que haya en el servidor.

Según la Open Web Application Security Project (Owasp), es desde ya casi diez años, la vulnerabilidad numero uno, de su [top diez](https://www.owasp.org/index.php/Top_10_2013-A1-Injection){:target="_blank"}. 




<figure>
<img alt="que es sql injection" class="img img-responsive" src="/resources/images/que-es-sql-injection/sql-injection.png"/>
<figcaption>
SQL Injection, la vulnerabilidad web más peligrosa según OWASP. 
</figcaption>
</figure>

## SQL Injection en la practica

Por ejemplo nuestra pagina web, paginaejemplo.com tiene un listado de coches por marca, donde nos muestra todos los coches de ferrari.

*www.paginaejemplo.com/cochespormarca?marca=ferrari*

cambiamos en el navegador la url y escribimos esto:

*www.paginaejemplo.com/cochespormarca?marca=ferrari' or 1=1- -*

Al ejecutar nos dara la lista de todos los coches que haya en el sistema. Y eso es porque hemos añadido *' or 1=1--*, y con eso hemos modificado el funcionamiento de la sql que ejecutara la base de datos. La sentencia SQL ha pasado de pedir solo los coches ferrari a pedir los coches ferrari o todos los coches que cumplan la condicion de que 1 es igual a 1, es decir ha pasado el listado de todos los coches.

<div class="env-header">SQL ORIGINAL</div>
{% highlight sql linenos %}

Select id, nombre from coches where marca = 'ferrari'

{% endhighlight %}

<div class="env-header">SQL CON SQL INJECTION</div>
{% highlight sql linenos %}

Select id, nombre from coches where marca = 'ferrari' 
or 1=1 --

{% endhighlight %}

### Y ese es su peligro, ¿mostrar todo el listado de coches? ...

Pues no, es solo para saber si la web puede ser vulnerable a SQL injection o inyeccion de SQL, imaginate si escribieramos si escribieramos algo estilo:

*www.paginaejemplo.com/cochespormarca?marca=ferrari' union select id, usuario from usuarios*

Ya entran sudores frios no?, y no solo eso, sino que con la vulnerabilidad de SQL Injection, se pueden modificar registros, borrar tablas e incluso crear nuevos usuarios en la base de datos SQL incluso afectar al servidor de SQL, es por eso que esta vulnerabilidad lleva diez años siendo la más peligrosa de todas las vulnerabilidades web que hay.

## ¿Y esto sigue pasando?

Si, es la vulnerabilidad web más peligrosa, facil de detectar y más comentada de todas, y a dia de hoy sigue pasando, por ejemplo, el 30 de diciembre del 2016, un [grupo de hackers españoles](http://la9deanon.tumblr.com/post/155170575049/haciendo-lulz-con-las-c%C3%A1maras-de-comercio-del){:target="_blank"} atacaron mediante SQL Injection varias webs de camaras de comercio de España (la camara de madrid, la de valencia, la de cantabria, la de alicante...).

En los proximos post ire escribiendo más en detalle como ejecutar estos ataques, incluso automatizarlos, y tambien como defenderse de ellos.









