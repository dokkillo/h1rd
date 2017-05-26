---
layout: post
title: Ataque XSS Reflejado
category: Hacking
comments: true
description: Cuando la web no da errores con las excepciones de la base de datos, cuando no es posible ni inyectar codigo por union ni siquiera por un ataque ciego si/no, lo unico que queda por probar es ataque ciego por tiempo. El más dificil de todos.
tags:
    - ethical hacker
    - XSS
    - owasp
---

Cuando la web no da errores con las excepciones de la base de datos, cuando no es posible ni inyectar codigo por union ni siquiera por un ataque ciego si/no, lo unico que queda por probar es ataque ciego por tiempo. El más dificil de todos.
Una situación donde se puede usar este ataque es cuando al ejecutar un proceso, por ejemplo, un comentario, no podemos controlar la respuesta que recibimos por lo tanto no podemos hacer un ataque ciego por si/no.