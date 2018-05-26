---
layout: post
title: Fase reconocimiento
category: Hacking
comments: true
description: Esta fase consiste en recopilar toda la información posible de nuestro objetivo, que seguramente la necesitaremos más adelante. Esta información consiste en conseguir las ips, nombres de usuario, trabajadores de la empresa, tipologias de red, tecnologias usadas, emails.

tags:   

    - pentesting

---

Esta fase consiste en recopilar toda la información posible de nuestro objetivo, que seguramente la necesitaremos más adelante. Esta información consiste en ips, nombres de usuario, trabajadores de la empresa, tipologias de red, tecnologias usadas, emails.
En esta fase hay que ponerse la ropa de detective y saber buscar, aunque no lo creais lo que se puede saber de la empresa solo buscando por internet.
Estas son las maneras para conseguir información de una empresa:

## Google Hacking

El todopoderoso buscador de internet Google, tendra muchos datos, y sera nuestra herramienta principal recabando datos, para ver más sobre [Google Hacking]({% post_url 2017-06-12-Google-hacking %}) 

## Pagina web de la empresa

En la pagina web de la empresa podemos encontrar muchos datos utiles, algunos a simple vista, por informacion pasada por ellos, otros mediante el analisis del codigo de la pagina, es increible lo facil que es dejarse un comentario revelador en los javascript o en los css.

## The Wayback Machine

En esta pagina web, tenemos snapshots de la web que queramos en diferentes momentos a lo largo de los años, con los datos que tienen guardados podemos analizar y encontrar datos que en un momento se mostraron al publico y luego se quitaron, por ejemplo un rooster con todos los empleados de la empresa que meses despues se quito por seguridad. [The Wayback Machine](https://archive.org/web/){:target="_blank"}. 

## Infojobs o paginas web de busqueda de trabajo

En infojobs o otras paginas webs de busqueda de trabajo, podemos encontrar que perfiles de trabajador estan buscando y con ello podemos saber las tecnologias (Administrador de red, experto en windows xp...), los requerimientos, el perfil de empleado y con ellos hacernos una imagen de que buscan.

## Linkedin

Si en la parte anterior podiamos ver que perfiles busca la empresa, para ver sus tecnologias, en linkedin podemos ver la gran mayoria de trabajadores y con ello saber quienes son, que experiencia y conocimientos tienen etc.

## Whois

Con el whois, podras ver todos los datos del registro del dominio, el email del registrador, sus datos personales, su movil. Se puede ver tanto por comando en linux o en windows escribiendo whois nombre-dominio o mediante la url [Whois](https://www.whois.com/whois/){:target="_blank"}. 
Hay una manera de que no puedan ver esto, y que la empresa pague una pequeña cantidad, unos 5-10€ anuales, y haga que esos datos queden ocultos.


