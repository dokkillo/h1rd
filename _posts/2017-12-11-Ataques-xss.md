---
layout: post
title: Ataques XSS
category: Hacking
comments: true
description: Cross-Site Scripting (XSS) es un tipo de ataque por inyección, donde un tercer usuario puede inyectar codigo javascript en una pagina web, provocando que la pagina realice funciones que ni el usuario ni el programdor web esperaban. Este grave problema surge cuando la aplicación web acepta lo que escribe el usuario sin validarlo ni codificarlo. En este blog ya hemos hablado anteriormente del xss, pero en este articulo, quiero entrar mucho más a fondo.
tags:   
    - hacker
    - owasp
    - xss

---

Cross-Site Scripting (XSS) es un tipo de ataque por inyección, donde un tercer usuario puede inyectar codigo javascript en una pagina web, provocando que la pagina realice funciones que ni el usuario ni el programdor web esperaban. Este grave problema surge cuando la aplicación web acepta lo que escribe el usuario sin validarlo ni codificarlo. En este blog ya hemos hablado anteriormente del xss, pero en este articulo, quiero entrar mucho más a fondo.

## Tipos de XSS

* XSS Persistido

Un xss persistido, consiste en que el codigo inyectado se guarda en el servidor, sea en base de datos, un log o en los comentarios, y después la victima al usuar la pagina web, tambien ejecuta ese codigo malicioso.

* XSS Reflejado

El xss reflejado se produce cuando la entrada del usuario es devuelta inmediatamente por una aplicación web en un mensaje de error, resultado de busqueda o cualquier otra respuesta que incluye parte o la totalidad de la entrada proporcionada por el usuario, sin que los datos sean seguros para renderizar en el navegador y sin almacenar permanentemente los datos proporcionados por el usuario.

* XSS en DOM o Tipo 0 XSS

Este tipo de xss fue definido por [Amit Klein en 2005](http://www.webappsec.org/projects/articles/071105.shtml){:target="_blank"}, esta bastante relacionado con el xss reflejado. Este tipo de ataque se produce cuando el payload o codigo malicioso modifica el DOM del navegador de la victima haciendo que funcione de una manera diferente, pero que la pagina en si mismo (el HTTP response) no cambie.
Un tipo de xss en DOM, puede ser enviar el payload en los fragments de la url ("#"), ya que esa parte nunca se envia al servidor. 

{% highlight sql linenos %}

http://www.some.site/page.html#default=Payload

{% endhighlight %}


## Ejemplos de XSS

Hasta ahora siempre los xss que he probado o ejecutado han sido los tipicos de añadir un script y un alert en un textbox y voilà, ya esta el xss, pero en la vida real, hay mucho más sitios donde encontrar y lanzar un xss. Yo he estado practicando xss en dos sitios, [Google XSS](https://xss-game.appspot.com/){:target="_blank"} y [Pentester Lab](https://pentesterlab.com/exercises/web_for_pentester){:target="_blank"}, os recomiendo ambos sitios para practicar cross-site scripting.
En esta parte del articulo ire poniendo sitios o apuntes donde buscar y ejecutar un xss.

* cross-site scripting en la url

Es el xss más basico y sencillo de todos, por ejemplo tenemos esta url:

{% highlight sql linenos %}

http://www.some.site/page.php?name=windows

{% endhighlight %}

cambiar el parametro "windows" por nuestro payload basico

{% highlight sql linenos %}

http://www.some.site/page.php?name=<script>alert(1)</script>

{% endhighlight %}
