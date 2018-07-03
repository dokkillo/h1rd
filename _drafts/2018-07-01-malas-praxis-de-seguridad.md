---
layout: post
title: Malas praxis de seguridad
category: Hacking
comments: true
description: El nivel de seguridad de un sistema es el nivel de seguridad del eslabón más debil, ¿que logica tiene usar sistemas superseguros, con un buen cifrado, con un buen codigo donde no hay vulnerabilidades, si despues el usuario puede ponerse como password 1234?. En este post detallare algunas de las malas praxis o malas practicas que he visto recientemente en paginas webs que he estado auditando.
tags:   

    - owasp
    - programacion

---

El nivel de seguridad de un sistema es el nivel de seguridad del eslabón más debil, ¿que logica tiene usar sistemas superseguros, con un buen cifrado, con un buen codigo donde no hay vulnerabilidades, si despues el usuario puede ponerse como password 1234?. En este post detallare algunas de las malas praxis o malas practicas que he visto recientemente en paginas webs que he estado auditando.

<figure>
<img alt="Fichero con los passwords más usados. Permitir usar passwords simples es una mala praxis de seguridad" class="img img-responsive" src="/resources/images/malas-praxis-seguridad-password"/>
<figcaption>
Fichero con los passwords más usados. Permitir usar passwords simples es una mala praxis de seguridad
</figcaption>
</figure>

## El password del usuario

Probablemente el talón de Aquiles de las mayorias de las aplicaciones informaticas, ya que el usuario suele ser un vago por naturaleza y no siente/entiende la necesidad de tener un password fuerte. El usuario siempre tendra el password lo más simple que el sistema le permita tenerlo, es decir si una aplicación web permite tener como password 1234, el usuario se pondra 1234.


