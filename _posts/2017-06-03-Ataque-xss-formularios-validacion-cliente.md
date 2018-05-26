---
layout: post
title: Ataque XSS en los formularios de solo validación cliente
category: Hacking
comments: true
description: La validación cliente en las paginas webs, es totalmente recomendable tanto para el servidor como para el usuario pero el problema llega cuando solo se valida al cliente y no se valida en el servidor, y con fiddler se puede pasar esa validación facilmente pudiendo dejar codigo xss persistido en la base de datos de la pagina web.
tags:   

    - owasp
    - xss
    - fiddler
---

La validación cliente en las paginas webs, es totalmente recomendable tanto para el servidor como para el usuario pero el problema llega cuando solo se valida al cliente y no se valida en el servidor, y con fiddler se puede pasar esa validación facilmente pudiendo dejar codigo xss persistido en la base de datos de la pagina web.


Según la Open Web Application Security Project (Owasp), es desde ya casi diez años, la vulnerabilidad numero tres, de su [top diez](https://www.owasp.org/index.php/Top_10_2013-A3-Cross-Site_Scripting_(XSS)){:target="_blank"}. 

## Para practicar

Te recomiendo que uses esta pagina web: [hackyourselffirst.troyhunt.com](http://hackyourselffirst.troyhunt.com){:target="_blank"}. Es una pagina vulnerable hecho a posta para poder probar todas las vulnerabilidades web de Owasp, esta creada por el hacker etico [Troy Hunt](https://www.troyhunt.com/){:target="_blank"}. 
Tiene varios cursos de hacking en [Pluralsight](https://app.pluralsight.com/library/){:target="_blank"} te recomiendo que te subscribas a Pluralsight y los hagas.

## Validaciones en cliente

Las validaciones de formularios en cliente mediante javascript es algo muy bueno, para empezar el codigo se valida en el browser del usuario si hay algun dato que falte o incorrecto, le sale una advertencia y le obliga a rectificar, con esto se consiguen menos llamadas al servidor y que la aplicación vaya más fluida.

Ejemplos de validaciones cliente en formularios:

{% highlight html linenos %}

   <div class="control-group">
      <label class="control-label" for="LastName">Last name</label>
      <div class="controls">
        <input data-val="true" data-val-length="The field Last name must be a string with a maximum length of 100." data-val-length-max="100" data-val-regex="Invalid Last name" data-val-regex-pattern="^([a-zA-Z]+)$" data-val-required="The Last name field is required." id="LastName" name="LastName" type="text" value="" />
      </div>


{% endhighlight %}

En el codigo html anterior, de una pagina hecha en ASP.NET, tenemos tres validaciones:

* el apellido tiene que ser menor de 100 caracteres
* el apellido no puede estar vacio
* el apellido solo puede estar compuesto de letras mayusculas o minusculas.


## Empezando la demostración

Para esta demostración necesitamos usar [Fiddler](http://www.telerik.com/fiddler){:target="_blank"} nos ayudara en la creación de los mensajes al servidor.
La idea del ataque es probar si un formulario de registro de usuarios tiene es vulnerable a xss. Asi que encendemos Fiddler y empezamos a crear un usuario normal, en el apellido intentamos añadir nuestro payload pero al tener la validacion en cliente que solo permite letras, no nos deja, asi que acabamos de registrar un usuario normal y sin problemas.

<figure>
<img alt="El formulario basico donde nos saltaremos las validaciones en cliente" src="/resources/images/xss/ataque-validacion-cliente.png"/>
<figcaption>
El formulario basico donde nos saltaremos las validaciones en cliente
</figcaption>
</figure>

Con Fiddler hemos capturado la peticion que hicimos al servidor al crear el usuario, asi que con el composer de Fiddler la editaremos y cambiaremos nuestro apellido por esto:

{% highlight html linenos %}

%3Cscript%3Ealert(%22hello%22)%3C%2Fscript%3E

{% endhighlight %}

que es simplemente un alert basico de javascript que dice hello, pero codificado para que las Urls lo acepten. Una recomendacion, acuerdate de __cambiar tanto el nombre del usuario como el password__ para que al registrar un nuevo usuario no te de problemas.

{% highlight html linenos %}

<script>alert("hello")</script>

{% endhighlight %}

<figure>
<img alt="Montando el ataque en XSS con ayuda de Fiddler" src="/resources/images/xss/ataque-validacion-cliente-fiddler.png"/>
<figcaption>
Montando el ataque en XSS con ayuda de Fiddler
</figcaption>
</figure>

Ya con el nuevo usuario, seria tan facil como logarnos como el, e ir a la pagina de votos de coche, y votar por un coche, cada vez que un usuario entre le saltara un popup.

<figure>
<img alt="Ataque XSS ejecutado y funcionando" src="/resources/images/xss/ataque-validacion-cliente-alert.png"/>
<figcaption>
Ataque XSS ejecutado y funcionando
</figcaption>
</figure>

Puede que un pop-up con hello, sea poco peligroso, pero se puede añadir codigo javascript que robe las sessiones de los usuarios, puedes añadir redirecciones que vayan a paginas maliciosas, o incluso, en un listado de paises añadir, un pais que no esta, esto podria hacer que la aplicación se rompiera ya que nunca encontrarian ese pais en el listado...






