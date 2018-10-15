---
layout: post
title:  Vulnerabilidad XML External Entity
category: Hacking
comments: true
description: La vulnerabilidad de XML External Entity o XXE (como se la conoce) se basa en un sistema deficiente al parsear los XMLs que recibe la aplicación web, permitiendo la inyección de entidades externas de XML posibilitando ataques como conseguir ficheros del servidor de producción o ejecucción de codigo. En el fondo, sucede igual que en el SQL inyection (SQLi) nunca te fies de lo que recibes del usuario.
tags:   

    - owasp
    

---

La vulnerabilidad de XML External Entity o XXE (como se la conoce) se basa en un sistema deficiente al parsear los XMLs que recibe la aplicación web, permitiendo la inyección de entidades externas de XML posibilitando ataques como conseguir ficheros del servidor de producción o ejecucción de codigo. En el fondo, sucede igual que en el SQL inyection (SQLi) nunca te fies de lo que recibes del usuario.

<figure>
<img alt="Fichero con los passwords más usados. Permitir usar passwords simples es una mala praxis de seguridad" class="img img-responsive" src="/resources/images/malas-praxis-seguridad-password"/>
<figcaption>
Fichero con los passwords más usados. Permitir usar passwords simples es una mala praxis de seguridad
</figcaption>
</figure>

## El password del usuario

Probablemente el talón de Aquiles de las mayorias de las aplicaciones informaticas, ya que el usuario suele ser un vago por naturaleza y no siente/entiende la necesidad de tener un password fuerte. El usuario siempre tendra el password lo más simple que el sistema le permita tenerlo, es decir si una aplicación web permite tener como password 1234, el usuario se pondra 1234.


