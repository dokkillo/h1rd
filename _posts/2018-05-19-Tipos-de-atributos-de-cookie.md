---
layout: post
title: Tipos de atributos de cookies
category: Hacking
comments: true
description: Las cookies o HTTP cookies consiste en que informacion enviada o recibida en cabeceras HTTP queda almacenada en el lado del cliente por un tiempo. El objetivo principal de las cookies era para facilitar el acceso de los usuarios a sus paginas web favoritas, pero actualmente se usan para muchas cosas y no todas son buenas.
tags:   
    - hacker
    - owasp
    - cookie

---

Las cookies o HTTP cookies consiste en que informacion enviada o recibida en cabeceras HTTP queda almacenada en el lado del cliente por un tiempo. El objetivo principal de las cookies era para facilitar el acceso de los usuarios a sus paginas web favoritas, pero actualmente se usan para muchas cosas y no todas son buenas.

<figure>
<img alt="El monstruo de las galletas" class="img img-responsive" src="/resources/images/cookie.png"/>
<figcaption>
El monstruo de las galletas
</figcaption>
</figure>

## Tipos de atributos

Las cookies tienen los siguientes atributos, en este articulo los enumerare y explicare las implicaciones de seguridad respecto cada atributo. Para ver las propiedades de las cookies hay que seguir los siguientes pasos:

* Abrimos el navegador Firefox, aunque estos pasos esten basados en firefox,seguramente en Chrome y Edge tengan opciones parecidas.
* Vamos al menus lateral y seleccionamos "Desarrollador web" y alli seleccionamos "Inspector de almacenamiento". Puedes ir directamente con el atajo "Mayus + F9".
* Y alli vemos el listado de cookies asociadas, ya solo nos queda pulsar sobre una cookie y ver el resto de propiedades.

<figure>
<img alt="Como ver las propiedades de una cookie" class="img img-responsive" src="/resources/images/como-ver-cookies-navegador.png"/>
<figcaption>
Como ver las propiedades de una cookie
</figcaption>
</figure>

### Atributo de cookie "Secure"

Este atributo obliga a que la cookie solo viaje a traves de conexiones https. Por ejemplo en una pagina web que tenga navegación por https, por ejemplo https://www.h1rd.com y te autentificas con ella, al hacerlo se genera una cookie con un token y esta no tiene la propiedad de secure puesta a true. Si por ejemplo se quita la "s", y al llamar a http://www.h1rd.com no redirige y sigue funcionando la web igual, esa cookie con el token de autentificacion queda visible y viajando a traves de http, por lo que cualquiera que este "viendo el trafico" podria coger el token y suplantarnos.

### Atributo de cookie "HttpOnly"

Este atributo va de la mano con el atributo anterior Secure. Este atributo al no estar puesto a true puede permitir que si un atacante consiguiera crear un xss, este podria la cookie con la propiedad HttpOnly a otra pagina web y almacenarla para asi luego poder acceder a su cuenta y sus datos.

### Atributo de cookie "Domain"

El atributo "domain" significa el dominio por el cual la cookie es valida y puede ser enviado en cada request para el dominio o el subdominio. Si este atributo no estuviera inicializado o puesto, el valor por defecto es el hostname de la web.

Esta propiedad es incluso más importante que la propiedad de "secure", ya que le dice al navegador web que la cookie solo puede ser enviada a los dominios que cumplan los requisitos. Uno de los temas curiosos es que hay navegadores web (Internet Explorer 2014) que implementan su propia [funcionalidad en la cookie de Domain, en contra de los RFCs](https://www.mxsasha.eu/blog/2014/03/04/definitive-guide-to-cookie-domains/){:target="_blank"} por lo que a veces podriamos ver que una vulnerabilidad no es explotable en Chrome pero si en firefox.

El problema de seguridad de este atributo de cookie, es que si el dominio al que apunta la cookie se viese comprometido por alguna razón, este haria nuestra web puediera tener problemas de seguridad ya que estariamos enviando cookies a una web insegura.

### Atributo de cookie "Path"

Este atributo, hace referencia a la URL o la ruta por la cual esta cookie es valida, el valor de este atributo por defecto es "/". Esta propiedad es bastante util cuando tenemos una aplicación web con multitud de webs o portales, y queremos que una cookie en particular solo funcione dentro de un determinado directorio. Por ejemplo "/admin", en este caso, la cookie deberia tener el atributo puesto como "/admin/", si por ejemplo le faltase la barra de detras, y solo estuviera como "/admin", podria hacer que un atacante creara un portal que se llamase /admin2 y esa cookie tambien se enviase alli, por lo tanto es una de cosas que hay que observar de este atributo.

### Atributo de cookie "Expires"

Este atributo va relacionado sobre la fecha con la que la cookie expira. Su valor por defecto es el tiempo que dure la sesion. Una de las cosas que tenemos que validar es que en las cookies con este atributo puesto no deben contener informacion importante para el usuario, tipo session tokens. Ya que si un atacante se pudiera hacer con esa cookie, podria logarse como el usuario. 

