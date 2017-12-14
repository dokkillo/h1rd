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

### Cross-site scripting en la url

Es el xss más basico y sencillo de todos, por ejemplo tenemos esta url:

{% highlight sql linenos %}

http://www.some.site/page.php?name=windows

{% endhighlight %}

cambiar el parametro "windows" por nuestro payload basico

{% highlight sql linenos %}

http://www.some.site/page.php?name=<script>alert(1)</script>

{% endhighlight %}

### Saltarse medidas de seguridad basicas contra xss

Imaginemos un caso, donde a un programador de una pagina web, le dicen que su pagina es vulnerable a un ataque por xss, el pobre programador que no sabe mucho de seguridad ve que pueden añadir javascript en su url, asi que lo que dedice es poner una expresion regular que si encuentra el tag script lo eliminara. ¿Cual es el problema? que si el atacante, en su payload en vez de poner script, pone sCript o sCRipt la validación no funciona.

Además no solo eso, si el payload contiene algo como esto,

{% highlight sql linenos %}

<scri<script>pt>

{% endhighlight %}


tambien pasaria, ya que al solo pasar la validación una vez, elimina los tags script, pero al eliminarlos se forman nuevos.

### Payload dentro de HTML

Puede que haya unas validaciones muy fuertes que bloqueen el tag script, pero si se permita añadir html, y con ello poder meter nuestro payload.

Ejemplos:

* En el tag img, al no tener una imagen correcta salta a la propiedad onerror donde esta nuestro alert haciendo que se ejecute.

{% highlight sql linenos %}

<img src='pppp' onerror='alert(1)' />

{% endhighlight %}

* En el tag div tenemos las propiedades onmouseover (hay que mover el ratón fuera)

{% highlight sql linenos %}

<div id="sub1" onmouseover="javascript:alert('1');">some text</div>

{% endhighlight %}

* Tambien con el tag div tenemos la propiedad onmousemove (mover el ratón), además de onmousemove y onmouseover se incluyen todas las demas propiedades relacionadas con [eventos de ratón](https://www.w3schools.com/tags/ref_eventattributes.asp){:target="_blank"} 

{% highlight sql linenos %}

<div id="sub1" onmousemove="javascript:alert('1');">some text</div>

{% endhighlight %}

* O la propiedad onclick dentro de div (dar a click dentro de el texto)

{% highlight sql linenos %}

<div id="sub1" onclick="javascript:alert('1');">some text</div>

{% endhighlight %}

* Además de el tag img o el tag div, tambien podemos usar el tag a de html donde usando las mismas propiedades que hemos visto antes.

{% highlight sql linenos %}

<a onmousemove="javascript:alert('1');">click here</a>

{% endhighlight %}

* O directamente creando un link, donde al pulsar el link ejecutamos el payload

{% highlight sql linenos %}

<a href='javascript:alert(1)'>click here</a>

{% endhighlight %}


### No todo es Alert

Puede que una web sea vulnerable a XSS pero el Alert este bloqueado, como hemos visto que se ha hecho anteriomente con la palabra script, pero además de alert tenemos otras opciones, no tan conocidas, pero el uso es el mismo, como prompt o confirm

{% highlight sql linenos %}

<script>prompt(1)</script>

{% endhighlight %}

{% highlight sql linenos %}

<script>confirm(1)</script>

{% endhighlight %}


## Recapitulando

xss everywhere, como hemos podido ver en este articulo, no solo hay xss en un textbox con un simple alert, sino hay muchisimas maneras de ejecutar un xss y en muchos sitios, si quieres más información detallada visita: [XSS Evasion Filter Cheat Sheet](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet){:target="_blank"} 
