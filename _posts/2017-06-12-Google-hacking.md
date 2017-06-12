---
layout: post
title: Google Hacking
category: Hacking
comments: true
description: En los ultimos años, todo el mundo sabe que si algo no esta en Google, es que no existe, lo que no sabe mucha gente, es que Google tiene varios comandos y maneras de buscar que nos pueden ayudar en nuestras tareas de busqueda, muchos crackers usan el buscador para encontrar webs vulnerables. Como pentester debemos ser capaces de ver nuestro target con esos mismos ojos. Aunque cualquier usuario avanzado de internet deberia conocer estos comandos.

tags:   
    - hacker
    - intro
---

En los ultimos años, todo el mundo sabe que si algo no esta en Google, es que no existe, lo que no sabe mucha gente, es que Google tiene varios comandos y maneras de buscar que nos pueden ayudar en nuestras tareas de busqueda, muchos crackers usan el buscador para encontrar webs vulnerables. Como pentester debemos ser capaces de ver nuestro target con esos mismos ojos. Aunque cualquier usuario avanzado de internet deberia conocer estos comandos.

## Busqueda de terminos

* __” ” (comillas): buscar frase exacta, por ejemplo "Calles de madrid"__

Por ejemplo al buscar *calles de madrid* no salen en Google, 16 Millones de resultados, pero al buscar por *\"calles de madrid\"* solo salen 400.000 ya que busca resultados con frases exactas a *calles de madrid*

* __\+ y -: incluir y excluir.__

Para buscar terminos y excluir o incluir otros terminos, por ejemplo queremos buscar Toledo pero excluir el termino Seat, para que no nos añada terminos como Seat Toledo.

Por ejemplo si buscamos toledo, nos aparecen 202k terminos
Si buscamos toledo -seat nos saldran solo los terminos relacionados con la ciudad de toledo, nos aparecen 195k terminos
Si buscamos toledo +seat, solo queremos terminos relacionados con el coche seat toledo, nos aparecen el resto de terminos.

* __\* (asterisco): comodín, cualquier palabra, pero una sóla palabra__

El ejemplo más facil para entender esto es "top * de las maravillas del mundo" y nos buscara las top 5 de las maravillas del mundo, el top 15 de las maravillas del mundo... 

* __AND y OR__ 

Operadores booleanos Y y OR que nos ayudaran en varias sentencias de busqueda.

* __\~__ 

Para buscar sinonimos de la palabra por ejemplo: *~barcos*

## Comandos avanzados

* __site:__

Con este comando solo buscaremos enlances de la pagina web, por ejemplo *site:h1rd.com*  RECUERDA: No debe haber espacio entre site: y la url que busques, o no te dara los resultados correctos.

* __filetype:  o ext:__ 

Con este comando podras buscar ficheros que terminen en la terminacion de ficheros que queramos.

por ejemplo:

*site:sans.org AND filetype:pdf* buscara todos los pdfs que haya en la pagina sans.org

* __intitle:__

Busca la palabra dentro del title, de la pagina, por ejemplo podriamos buscar algo asi:

*intitle:SEO*

* __inurl:__

Busca la palabra dentro de la url

## ¿Y esto que tiene que ver con hacking?

Pues imaginad que hay una vulnerabilidad en el CMS de Magento, y sabemos que los portales Magento tienen esta firma : *"Magento is a trademark of Magento Inc."* seria tan facil como ir a google y buscar:

*"Log in" "Magento is a trademark of Magento Inc."*

Y si quisieramos passwords...

*"INSERT INTO phpbb_users" ext:sql*

Pues como veis todo esto es Google Hacking es algo bastante peligroso, y es muy necesario e importante saber en nuestras webs que estamos exponiendo.

Para más informacion sobre google hacking, en [Google Hacking DB](https://www.exploit-db.com/google-hacking-database/){:target="_blank"} podras encontrar más ejemplos de busquedas peligrosas.







