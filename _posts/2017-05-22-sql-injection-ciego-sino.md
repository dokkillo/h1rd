---
layout: post
title: Ataque SQL Injection ataque si/no o boleano
category: Hacking
comments: true
description: Es el ataque de sql injection más complicado, ya que puede ser que no podamos hacer el ataque por error ni tampoco por union, y como si fuera un fantasma en una casa encantada, solo podamos preguntar preguntas cuya respuesta sea verdadero o falso. De este ataque hay dos tipos, si/no y por tiempo. En este articulo hablaremos del ataque si/no o boleano
tags:
    - injection
    - hacker
    - owasp
---

Es el ataque de sql injection más complicado, ya que puede ser que no podamos hacer el ataque por error ni tampoco por union, y como si fuera un fantasma en una casa encantada, solo podamos preguntar preguntas cuya respuesta sea verdadero o falso. De este ataque hay dos tipos, si/no y por tiempo. En este articulo hablaremos del  ataque si/no o boleano

<figure>
<img alt="que es sql injection" class="img img-responsive" src="/resources/images/que-es-sql-injection/sql-injection.png"/>
<figcaption>
SQL Injection, la vulnerabilidad web más peligrosa según OWASP. 
</figcaption>
</figure>


## Para practicar

Te recomiendo que uses esta pagina web: [hackyourselffirst.troyhunt.com](http://hackyourselffirst.troyhunt.com){:target="_blank"}. Es una pagina vulnerable hecho a posta para poder probar todas las vulnerabilidades web de Owasp, esta creada por el hacker etico [Troy Hunt](https://www.troyhunt.com/){:target="_blank"}. 
Tiene varios cursos de hacking en [Pluralsight](https://app.pluralsight.com/library/){:target="_blank"} te recomiendo que te subscribas a Pluralsight y los hagas.

## Entendiendo los ataques ciego por SI/NO

Puede que nos encontremos en una situacion, donde se ha programado correctamente una aplicacion web para que no de detalles del error, adios errores detallados dandonos los nombres de las tablas y las tarjetas de credito de los usuarios, y que por motivos de la sentencia sql que se este ejecutando no podamos usar el union.

La sentencia original es esta y nos da el resultado de un listado de coches

<div class="info alert">
http://hackyourselffirst.troyhunt.com/Supercar/Leaderboard?orderBy=PowerKw&asc=false
</div>

Si cambiaramos PowerKw por por ejemplo (select top 1 password from userprofile), nos aparecen los coches ordenados, da igual la manera, pero si buscamos por por supercarId2, que no existira, nos saldra un error de aplicación. Y es alli donde podemos ejecutar nuestro ataque ciego.

Tambien en este caso lo que podemos hacer, en vez de buscar por una columna que no exista, podemos buscar por otra columna que nos dara unos resultados distintos, asi no llamara tanto la atencion ya que no saldran errors en el log de la aplicacion.

## Creando la consulta para un ataque ciego SI/NO

Lo que haremos para explotar esta vulnerabilidad es un case sql tal como este:

<div class="env-header">CASE SQL</div>
{% highlight sql linenos %}

select * from supercar order by
case when (select count(*) from sys.tables) = 10
then powerkw else topspeedkm end desc

{% endhighlight %}

*select * from supercar order by* es como creemos que es la sentencia sql original

(select count(*) from sys.tables) = 10 es nuestra pregunta de si o no, si tiene 10 tablas sera si y nos mostrara el listado de coches ordenados por potencia, si es no, nos lo dara ordenado por velocidad.

A partir de aqui ya podriamos crear sentencias sql para preguntar sobre la base de datos, por ejemplo si la primera tabla se llama XXX o algo asi, aunque lo mejor seria hacer preguntas más genericas como, *empieza por m la primera tabla de la base de datos?* 


<div class="env-header">¿Empieza por M la primera tabla de la base de datos?</div>
{% highlight sql linenos %}

select * from supercar order by
case when (select top 1 substring(name,1,1) from sys.tables) = 'm'
then powerkw else topspeedkm end desc

{% endhighlight %}

El problema que esto es un proceso muy laborioso, ya que habria que preguntar 26 veces (una por letra), por posicion y por tabla, una eternidad vamos, mejor probar otro enfoque, en vez de usar letras, usar los valores ASCII, al ser numeros podremos preguntar si es menor de 109 (es la m).

{::options parse_block_html="true" /}

<figure class="table">

| Letra    | Valor | Letra | Valor |
| ------------- | ------------- | ----------- | -------- |
| a      | 97      | n  | 110  |
| b      | 98      | o   | 111   |
| c      | 99      | p   | 112   |
| d      | 100     | q   | 113   |
| e      | 101     | r  | 114   |
| f      | 102     | s   | 115   |
| g      | 103     | t   | 116   |
| h      | 104      | u   | 117   |
| i      | 105     | v   | 118   |
| j      | 106     | w   | 119   |
| k      | 107     | x   | 120   |
| l      | 108     | y   | 121   |
| m      | 109     | z   | 122   |


<figcaption>
**Table 1:** Tabla ASCII. 
</figcaption>
</figure>


{::options parse_block_html="false" /}

Lo que haremos sera preguntar, si la primera letra es menor o igual a 109 (es la mitad), si dicen que si, preguntaremos si la letr es menor o igual a 103 (la g es la mitad entre a y b) y asi hasta saber la primera letra, y con solo cinco querys sabremos la primera letra de la tabla, es laborioso pero mucho más rapido.


<div class="env-header">¿Empieza por 109 la primera tabla de la base de datos?</div>
{% highlight sql linenos %}

select * from supercar order by
case when (select top 1 ascii(lower(substring(name,1,1))) from sys.tables) <=109
then powerkw else topspeedkm end desc

{% endhighlight %}

Es muy laborioso pero pregunta a pregunta se puede ir conociendo todos los datos de la base de datos. Hay aplicaciones que automatizan estos procesos pero es necesario conocer como funcionan internamente.

