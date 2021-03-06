---
layout: post
title: Tipos de ataque de SQL Injection
category: Hacking
comments: true
description: Hay varios tipos de ataque de SQL Injection, algunos son bastante fáciles otros algo más complicados pero todos igual de peligrosos.
tags:
    - injection
    - owasp
---

En SQL Injection hay tres tipos de ataques principales, sql injection por error, por union y ataque ciego.


<figure>
<img alt="que es sql injection" class="img img-responsive" src="/resources/images/que-es-sql-injection/sql-injection.png"/>
<figcaption>
SQL Injection, la vulnerabilidad web más peligrosa según OWASP. 
</figcaption>
</figure>

## Ataque SQL Injection por error

Es el más común y el más fácil de explotar ya que es la propia aplicación que nos va diciendo los errores que da la base de datos cuando vamos usando los ataques de sql injection. Con este error es muy fácil conseguir cualquier cosa de la base de datos (estructura, tablas, nombres de campos e incluso datos).

## Ataque SQL Injection por union

Este ataque consiste en que una pagina devuelve un resultado, por ejemplo todos los restaurantes de comida japonesa de Madrid, es aquí donde el atacante añade al resultado original el resultado de otra query, por ejemplo, todos los usuarios y passwords de la web, y hace que ambas querys salgan en esa pagina de resultados.

## Ataque SQL Injection ciego

Este ataque es el más complicado y avanzado, es la tercera via, cuando ni el ataque por error ni el ataque por union funcionan, tenemos que ser creativos y tenemos que ir preguntando a la base de datos mediante si o no todo lo que necesitemos saber.
Hay dos tipo de ataque ciego:

-una basada en contenido, es decir, muéstrame el resultado correcto, los restaurantes japoneses de Madrid, si tengo razón, sino la tengo no me los muestres.

-basada en tiempo, tarda 5 segundos en mostrarme los resultados japoneses si tengo razón, sino muestra los al momento.


## Más información

Si quieres leer más información sobre SQL Injection puedes consultar otros post en nuestra sección sobre [SQL Injection](https://www.h1rd.com/tags/injection)







