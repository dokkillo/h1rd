---
layout: post
title: Ataque por referencia insegura de objetos
category: Hacking
comments: true
description: Este ataque referencia directa a objetos ("direct object reference") ocurre cuando un desarrollador expone una referencia hacia un objeto interno de la aplicación, (parametro web, formulario, fichero, base de datos). Un atacante podría cambiar estas referencias y acceder a otros recursos de la aplicacion sin autorización


tags:   
    - hacker
    - owasp
---

Este ataque referencia directa a objetos ("direct object reference") ocurre cuando un desarrollador expone una referencia hacia un objeto interno de la aplicación, (parametro web, formulario, fichero, base de datos). Un atacante podría cambiar estas referencias y acceder a otros recursos de la aplicacion sin autorización

Según la Open Web Application Security Project (Owasp), el ataque por referencia insegura de objetos forma parte de su [top diez](https://www.owasp.org/index.php/Top_10_2013-A4-Insecure_Direct_Object_References){:target="_blank"}. 

## Como funciona este ataque

Al entrar en nuestra pagina de datos personales de la web vulnerable aparecen nuestros datos correctamente, y mediante [Fiddler]({% post_url 2017-06-05-Fiddler %}), vemos que la llamada al server es:

 <div class="env-header">Url enviada al servidor</div>
{% highlight html linenos %}

www.webvulnerable.com/usuario?user=testUser

{% endhighlight %}

Asi que con Fiddler cambiamos la peticion HTTP y probamos diferentes opciones:

 <div class="env-header">Url enviadas al servidor</div>
{% highlight html linenos %}

www.webvulnerable.com/usuario?user=admin
www.webvulnerable.com/usuario?user=usuario1
www.webvulnerable.com/usuario?user=50002

{% endhighlight %}

Y con alguna de esas peticiones, si en alguna de esas peticiones recibieramos los datos del usario es que la web es vulnerable a un ataque por referencia insegura de objetos.

## ¿Porque sucede?

Este ataque sucede porque en la aplicación web no se controla el control de acceso,  es decir controlar que de verdad el usuario que pide algo, tiene de verdad permisos para verlo. Es decir no puedes ver los datos personales de otro usuario, si no eres ese usuario (O eres un administrador...)



