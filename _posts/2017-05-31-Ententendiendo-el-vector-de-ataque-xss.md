---
layout: post
title: Entendiendo el vector de ataque XSS
category: Hacking
comments: true
description: El vector de ataque XSS o Cross Site Scripting, es una de las vulnerabilidades más extendidas en las paginas web, según OWASP es la tercera en importancia en su TOP 10. Esta vulnerabilidad consiste en que un atacante es capaz de inyectar codigo javascript en una pagina visitada por el usuario y poder secuestrar la sesion del usuario o comprometer su navegador web.
tags:
    - hijacking
    - hacker
    - owasp
    - xss
    - intro
---

 El vector de ataque XSS o Cross Site Scripting, es una de las vulnerabilidades más extendidas en las paginas web, según OWASP es la tercera en importancia en su TOP 10. Esta vulnerabilidad consiste en que un atacante es capaz de inyectar codigo javascript en una pagina visitada por el usuario y poder secuestrar la sesion del usuario o comprometer su navegador web.

Según la Open Web Application Security Project (Owasp), es desde ya casi diez años, la vulnerabilidad numero tres, de su [top diez](https://www.owasp.org/index.php/Top_10_2013-A3-Cross-Site_Scripting_(XSS)){:target="_blank"}. 

Esta vulnerabilidad puede ser de dos tipos:

* Reflejada : el ataque requiere que el usuario visite un link de la pagina modificado por el atacante donde viene incrustado el payload o codigo malicioso.

* Persistente : el atancante es capaz de guardar su payload en la base de datos de la propia web (por ejemplo un comentario de un wordpress) y que cada vez que un usuario visitara esa pagina web, el ataque se lanzara.

## ¿Como detectarla?


Por ejemplo en una pagina web *miejemplo.com* que tiene un buscador y la url  es algo como *miejemplo.com/buscar?query=lechugas* y nosotros escribimos algo como esto:


{% highlight html linenos %}

miejemplo.com/buscar?query=<b>lechugas</b>

{% endhighlight %}

Y nos aparece en la pagina: usted esta buscando __lechugas__ es decir ha puesto la busqueda en negrita.

O si ponemos javascript:

{% highlight html linenos %}

miejemplo.com/buscar?query=<script><alert>soy vulnerable a xss</alert></script>

{% endhighlight %}

Y nos lanza un popup con ese mensaje, es que la web es vulnerable a XSS....




