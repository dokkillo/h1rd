---
layout: post
title: Ataque por Cross Site Request Forgery (CSRF)
category: Hacking
comments: true
description: El ataque por CSRF o XSRF, consiste en forzar al usuario a ejecutar peticiones no deseadas en una web, en la que estan autentificados, si que este se de cuenta. En este tipo de ataque es necesaria la utilización de ingenieria social para engañar a la victima y que ejecute la petición falsa, sea mediante un email, o un link de una red social.
tags:   
    - hacker
    - owasp
---

El ataque por CSRF o XSRF, consiste en forzar al usuario a ejecutar peticiones no deseadas en una web, en la que estan autentificados, si que este se de cuenta. En este tipo de ataque es necesaria la utilización de ingenieria social para engañar a la victima y que ejecute la petición falsa, sea mediante un email, o un link de una red social.

Según la Open Web Application Security Project (Owasp), el Cross Site Request Forgery forma parte de su [top diez](https://www.owasp.org/index.php/Top_10_2017-A8-Cross-Site_Request_Forgery_(CSRF)){:target="_blank"}. 

## Como funciona este ataque

Lo principal para ejecutar este ataque, es que el __usuario este autentificado__ en la pagina web a la que se va a atacar, y mediante ingenieria social la pagina web maliciosa simplemente reprodouce un request valido y correcto para la pagina web atacada.

Estamos aburridos en el trabajo y nos ponemos a mirar nuestro banco de total confianza Banco Vulnerable, hemos visto que nos han descontado más dinero de lo normal en un credito, luego llamaremos, como seguimos aburridos, vamos a ver nuestro facebook, y alli vemos un post de *¿Que eras en tu vida anterior?, Adivinalo* y lo pinchamos. La proxima vez que vayamos a ver nuestro gran banco, El Banco vulnerable, nos faltaran 1000€ y eso??...

Por ejemplo:

<div class="env-header">HTML para web que explota el CSRF</div>
{% highlight html linenos %}

<form action="http://bancoVulnerable.com" method="post" target="csrfFrame">
    <input type="hidden" name="AccountDest" value="00000-303232"/>
    <input type="hidden" name="Money" value="1000"/>
    <input type="submit" value="win" onclick="alert('En tu vida anterior fuistes un caballero de la mesa redonda')"/>
</form>
<iframe name="csrfFrame" style="visibility: hidden"></iframe>

{% endhighlight %}

### Que paso?

en la linea 1, vemos que es un formulario que hara un post a bancovulnerable con los campos que necesita, es un request totalmente valido y nosotros ya estabamos autentificados, ademas en la linea 6, el resultado del formulario sea correcto o no, se nos oculta.

## ¿Como protegerse?

Los ataques CSRF funcionan porque son predecibles, simplemente es reconstruir un request, para evitar esto, se añade un factor aleatorio mediante un CSRF token, que consiste en un string aleatorio entre la pagina legitima y el navegador via cookie.
Con esto, el ataque anterior no hubiese funcionado ya que no hubiera tenido el token correcto.

## Video de un ataque CSRF 

Este video es la prueba de concepto que realizo el ponente [Eduardo Sánchez](https://twitter.com/eduSatoe){:target="_blank"} en la Hack & Beers de Madrid

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZpXFHYK8Idk?rel=0" frameborder="0" allowfullscreen></iframe>
