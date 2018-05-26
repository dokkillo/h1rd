---
layout: post
title: Ataque por toma de control de un subdominio o subdomain takeover
category: Hacking
comments: true
description: El ataque de toma de control de un subdominio (o subdomain takeover en ingles) es una vulnerabilidad facil de detectar si sabes lo que estas buscando y muy peligrosa para la empresa en si mismo. Y os puedo asegurar que no es una vulnerabilidad unicornio de las que se encuentran una cada cinco años, sino que suelen pasar, yo mismo en la auditoria web que estoy haciendo esta semana me la encontre.
tags:   
    - hacker
    - owasp
    - subdominio

---

El ataque de toma de control de un subdominio (o subdomain takeover en ingles) es una vulnerabilidad facil de detectar si sabes lo que estas buscando y muy peligrosa para la empresa en si mismo. Y os puedo asegurar que no es una vulnerabilidad unicornio de las que se encuentran una cada cinco años, sino que suelen pasar, yo mismo en la auditoria web que estoy haciendo esta semana me la encontre.

<figure>
<img alt="Una pagina 404 por defecto de Github" class="img img-responsive" src="/resources/images/domain-takeover.png"/>
<figcaption>
Una pagina 404 por defecto de Github
</figcaption>
</figure>

## Que es un subdomain takeover o toma de control de subdominio

Esto se produce cuando un subdominio (por ejemplo idea.h1rd.com) apunta a un hosting por ejemplo (Github pages, Heroku, wordpress u otros hostings) y ese sitio ha sido borrado o nunca se llego a usar. 

Por experiencia es algo bastante normal ya que el departamento de desarrollo, muchas veces no gestiona los dominios, ya que eso suele ocuparse el departamento de IT o infrastructura, y a veces pasa que el equipo de desarrollo elimina una web o un recurso, y nunca avisa al departamento de infrastuctura o si le avisan pero nunca se llega a hacer, en definitiva se queda un subdominio apuntando a un servicio donde no hay nada esperandolo, esto permite que cualquiera se pueda hacer una pagina de github o del servicio que este apuntando el subdominio y reclamar el subdominio como suyo, por ejemplo en github pages es tan facil como crear un fichero CNAME con el subdominio que queremos usar.

## Como usar esta vulnerabilidad

Hay varias opciones para usar esta vulnerabilidad:

* bypass de medidas de seguridad asociadas al dominio (por ejemplo mediante cookies, [ver el articulo sobre tipos de atributos de cookies]({% post_url 2018-05-19-Tipos-de-atributos-de-cookie %}))

* Se pueden crear un sitio de phising, ya que se puede copiar la imagen de la pagina web y trabajar en su nombre.

* Operaciones de black SEO, se puede crear un blog o pagina web con la misma imagen de la pagina web y usar su nombre para hablar muy bien sobre nuestra pagina, por ejemplo, tener un subdominio de una web bien posicionada sobre turismo, nos daria muchos puntos si hablase bien de nuestra pagina cliente, un hotel.


## Como detectar un subdomain takeover o toma de control de subdominio

Es algo bastante sencillo, hay que encontrar los subdominios, o mediante Google Hacking o usando enumeradores de dominio como Enumall o Sublist3r puedes ver más información de como hacerlo, en el articulo que escribi sobre este tema en [Enumeración de subdominios]({% post_url 2018-05-07-Enumeracion-de-subdominios %})

## Como arreglar esta vulnerabildad

Esta vulnerabilidad es bastante facil de solventar, simplemente hay que entrar en la pagina donde tenemos alojado nuestro dominio, y quitar la entrada DNS que apunta a nuestra web eliminada.

## Subdomain takeover o toma de control de subdominio en el mundo real

Por ejemplo, uno de los casos que más me llamo la atención fue un articulo escrito en Medium, sobre como un Hacker gano 4500$ encontrando esta vulnerabilidad en la pagina web de Uber, o sea, es una vulnerabilidad bien pagada y puede pasar en todas las empresas sea Uber o sea la carniceria de abajo de casa.

Puedes leer el articulo en [4500$, Como tuve suerte](https://medium.com/bugbountywriteup/4500-bounty-how-i-got-lucky-99d8bc933f75){:target="_blank"}







