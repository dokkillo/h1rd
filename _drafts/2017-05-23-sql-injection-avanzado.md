---
layout: post
title: Ataque SQL Injection avanzado
category: Hacking
comments: true
description: Cuando la web no da errores con las excepciones de la base de datos, cuando no es posible ni inyectar codigo por union ni siquiera por un ataque ciego si/no, lo unico que queda por probar es ataque ciego por tiempo. El más dificil de todos.
tags:
    - sql injection
    - ethical hacker
    - owasp
---

Cuando la web no da errores con las excepciones de la base de datos, cuando no es posible ni inyectar codigo por union ni siquiera por un ataque ciego si/no, lo unico que queda por probar es ataque ciego por tiempo. El más dificil de todos.
Una situación donde se puede usar este ataque es cuando al ejecutar un proceso, por ejemplo, un comentario, no podemos controlar la respuesta que recibimos por lo tanto no podemos hacer un ataque ciego por si/no.

<figure>
<img alt="que es sql injection" src="/resources/images/que-es-sql-injection/sql-injection.png"/>
<figcaption>
SQL Injection, la vulnerabilidad web más peligrosa según OWASP. 
</figcaption>
</figure>


## Para practicar

Te recomiendo que uses esta pagina web: [hackyourselffirst.troyhunt.com](http://hackyourselffirst.troyhunt.com){:target="_blank"}. Es una pagina vulnerable hecho a posta para poder probar todas las vulnerabilidades web de Owasp, esta creada por el hacker etico [Troy Hunt](https://www.troyhunt.com/){:target="_blank"}. 
Tiene varios cursos de hacking en [Pluralsight](https://app.pluralsight.com/library/){:target="_blank"} te recomiendo que te subscribas a Pluralsight y los hagas.

## Software necesario

Al contrario de los otros ataques en este caso, es necesario, que no solo usemos el navegador web sino que tambien necesitamos la aplicacion [Fiddler](http://www.telerik.com/fiddler){:target="_black"} espero que en unos dias escriba algun curso de como funciona este programa. Actualizare este post con el enlace.


## El ataque SQL Injection por tiempo

Capturamos la peticion que hemos hecho a la web desde fiddler y con ella con el composer la vamos a modificar para asi poder enviar lo que nosotros necesitamos.

<figure>
<img alt="web vulnerable a sql injection" src="/resources/images/injection-time/injection-sql-time.png"/>
<figcaption>
Fiddler ayudandonos con el ataque de sql injection. 
</figcaption>
</figure>

Asi que cogeremos la sentencia sql del ataque ciego por si/no y la modificaremos un poco para adaptarla a lo que necesitamos.

<div class="env-header">IF SQL</div>
{% highlight sql linenos %}

'); if(select top 1 ascii(lower(substring(name,1,1))) from sys.tables) <=109 waitfor delay '00:00:05' --

{% endhighlight %}

En este caso usamos un if en vez de un case, ya que nos interesa que siga todo igual si nuestra pregunta es falsa, y que se retrase 5 segundos si nuestra pregunta es verdadera.
Tambien usamos '); para cerrar la query anterior que fue el comentario que preguntamos.

Y al ejecutar la sentencia depende de la respuesta a nuestra pregunta, tardara 5 segundos en responderse o sera instantaneo.


