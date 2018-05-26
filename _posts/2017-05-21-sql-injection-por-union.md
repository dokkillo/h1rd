---
layout: post
title: Ataque SQL Injection por union
category: Hacking
comments: true
description: Es la más visual de los ataques de sql injection, ya que consiste en añadir una sentencia sql maliciosa a la sentencia sql original haciendo que la web nos muestre más datos de los que tendria que mostrarnos.
tags:
    - injection

    - owasp
---

Es la más visual de los ataques de sql injection, ya que consiste en añadir una sentencia sql maliciosa a la sentencia sql original haciendo que la web nos muestre más datos de los que tendria que mostrarnos.
Puede ser que no sea posible hacer ataques por error, ya que los programadores hayan desactivado, logicamente, que se muestren esos errores en la pagina web.Si es asi,la otra manera es hacer este ataque.

<figure>
<img alt="que es sql injection" class="img img-responsive" src="/resources/images/que-es-sql-injection/sql-injection.png"/>
<figcaption>
SQL Injection, la vulnerabilidad web más peligrosa según OWASP. 
</figcaption>
</figure>


## Para practicar

Te recomiendo que uses esta pagina web: [hackyourselffirst.troyhunt.com](http://hackyourselffirst.troyhunt.com){:target="_blank"}. Es una pagina vulnerable hecho a posta para poder probar todas las vulnerabilidades web de Owasp, esta creada por el hacker etico [Troy Hunt](https://www.troyhunt.com/){:target="_blank"}. 
Tiene varios cursos de hacking en [Pluralsight](https://app.pluralsight.com/library/){:target="_blank"} te recomiendo que te subscribas a Pluralsight y los hagas.

## Como encontrar encontrar esta vulnerabilidad

En la pagina de hackyourselffirst.troyhunt.com en la pagina de buscar cilindros, y seleccionamos los coches que tienen 8 cilindros, logicamente solo nos saldran los coches con 8 cilindros.

<div class="info alert">
http://hackyourselffirst.troyhunt.com/CarsByCylinders?Cylinders=V8
</div>

Para ver si esta pagina es vulnerable a un ataque sql inject, solo haria falta añadir detras esto: ' or 1=1 --

<div class="info alert">
http://hackyourselffirst.troyhunt.com/CarsByCylinders?Cylinders=V8' or 1=1 --
</div>

y Tachan!! nos aparecen todos los coches,la pagina es vulnerable al ataque sql injection.


## SQL Injection por union

En la pagina anterior, ya vimos que era vulnerable a sql pero no es vulnerable a sql por error, es decir lo que vimos en el otro articulo no funciona, por lo que tenemos que cambiar de enfoque. Como podemos ver en la imagen, por defecto solo salen tres coches.

<figure>
<img alt="web vulnerable a sql injection" class="img img-responsive" src="/resources/images/injection-union/injection-union1.png"/>
<figcaption>
Esta web es vulnerable a sql injection, pero no el enfoque de sql injection por error
</figcaption>
</figure>

Ahora vamos a añadir esta sentencia y la vamos a enlazar mediante union a la sentencia original. Y unira ambos resultados. __esto solo funciona si ambas consultas devuelven los mismos resultados, en este caso un numero y un string__

<div class="env-header">Esta sentencia devuelve id y nombre.</div>
{% highlight sql linenos %}

select object_id, name from sys_tables

{% endhighlight %}

<figure>
<img alt="web vulnerable a sql injection donde se le añade nuestra query a la query del sistema"  class="img img-responsive" src="/resources/images/injection-union/injection-union2.png"/>
<figcaption>
web vulnerable a sql injection donde se le añade nuestra query a la query del sistema
</figcaption>
</figure>

Ya tenemos el nombre de las tablas mediante sys.tables, de alli podriamos sacar las columnas de cada tabla, sus valores etc...   asi funciona un ataque de sql injection mediante union.

