---
layout: post
title: Persistiendo la información sobre HTTP
category: Redes
comments: true
description: El protocolo HTTP es un protocolo sin estado, es decir cuando nos autenticamos en un sitio, en el proximo request que hacemos a la web, no viene ningún sitio del request que diga que estamos autenticados, por lo que tenemos que apañarnos con "algunas trampas". Cuando un usuario se identifica en un web, esta le envia un token, que es unico para el usuario, y asi cada vez que el usurio haga un request a la web, este token ira en el request para que la web sepa quien es el usuario.
tags:
    - hijacking

    - owasp
    - intro
    - protocolos
    - HTTP
---


El protocolo HTTP es un protocolo sin estado, es decir cuando nos autenticamos en un sitio, en el proximo request que hacemos a la web, no viene ningún sitio del request que diga que estamos autenticados, por lo que tenemos que apañarnos con "algunas trampas".
Cuando un usuario se identifica en un web, esta le envia un token, que es unico para el usuario, y asi cada vez que el usurio haga un request a la web, este token ira en el request para que la web sepa quien es el usuario.

## Persistiendo la información sobre HTTP

Hay tres maneras de guardar los datos de la sesión de un usuario, en la memoria del servidor (como ASP.NET por defecto), es decir cuando el servidor web se reinicia todos los datos de sesion del usuario desaparecen, tambien se pueden guardar en el servidor, mediante un proceso independiente que dedicado a persistir el estado del usuario, o en la base de datos.

En cada request de un usuario identificado hay un token que conduce a unos datos especificos al usuario guardados en alguna de las tres maneras posibles, si un usuario consigue datos de sesion de otro usuario, se produciria un secuestro de sesion (session hijacking).

Ese token /session id /auth cookie hay varias maneras de persistirlo para el usuario, a traves de cookies, a traves de la url o a traves de un formulario oculto.

## Persistiendo la sesion del usuario sobre las cookies

Una de las maneras para persitir ese session id que el usuario envia en cada request a la web es mediante cookies, que se quedan almacenadas en el navegador web. Las cookies tienen Pros y Contras:

__PROS__

* Las cookies se persisten en cada request
* las cookies persisten incluso si se cierra el navegador
* las cookies no aparecen en los logs, urls etc..

__CONTRAS__

* las cookies son vulnerables a los ataques de cross site scripting (XSS)
* las cookies solo permiten una sesion por navegador

## Persistiendo la sesion del usuario sobre URL

Otra de las maneras de persistir el session id del usuario es que este en la url que envia este al servidor, como con las cookies tambien tiene sus pros y sus contras:

__PROS__

* Este sistema permite multiples sesiones en un mismo navegador, ya que al estar referenciadas por url, solo afectan al tab del navegador.
* Funciona incluso cuando el cliente tiene las cookies desactivadas.

__CONTRAS__

* Session ID se pierde al cerrar el navegador.
* Session ID se envia en las url para pedir incluso recursos externos.
* Los session ID se quedan guardados en el historico del navegador, o en los logs del sistema incluso en los proxys donde pase el request.

## Persistiendo la sesion en formulario oculto

Consiste en pasar tu session Id a traves de un formulario oculto de la pagina, es una tecnica ya poco usuada estos dias, tambien tiene sus pros y contras:

__PROS__

* Este sistema permite multiples sesiones en un mismo navegador, ya que al estar referenciadas por url, solo afectan al tab del navegador.
* Funciona incluso cuando el cliente tiene las cookies desactivadas.

__CONTRAS__

* Session ID se pierde al cerrar el navegador.
* Cada request tiene que ser un POST (ya que el session ID se pierde con los GET)
* Al no poder usar el GET no es posible acceder embeidos en la pagina como videos, imagenes...












