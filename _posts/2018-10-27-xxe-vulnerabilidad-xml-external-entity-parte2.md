---
layout: post
title:  Empezando con XML External Entity (XXE 2)
category: Hacking
comments: true
description: Como vimos en el primer articulo de la serie sobre XXE, la vulnerabilidad de XML External Entity o XXE (como se la conoce) se basa en un sistema deficiente al parsear los XMLs que recibe la aplicación web, en este post veremos como ejecutar un ataque para explotar esta vulnerabilidad. 
tags:   

    - owasp
    - xxe
    
---

Como vimos en el primer articulo de la serie sobre XXE, la vulnerabilidad de XML External Entity o XXE (como se la conoce) se basa en un sistema deficiente al parsear los XMLs que recibe la aplicación web, en este post veremos como ejecutar un ataque para explotar esta vulnerabilidad. 

<figure>
<img alt="Ejemplo de un ataque usando la vulnerabilidad Xml External Entity (XXE)" class="img img-responsive" src="/resources/images/xxe_ejemplo_xml_external_entitity2.jpg"/>
<figcaption>
Ejemplo de un ataque usando la vulnerabilidad Xml External Entity (XXE)
</figcaption>
</figure>

### Atacando un XML External Entity (XXE)

Para nuestras pruebas de como explotar un XXE usaremos WebGoat 8.0 en su sección de XXE y para interceptar y modificar las peticiones usaremos BurpSuite. Puedes descargarte el CTF WebGoat en [su pagina de github](https://github.com/WebGoat/WebGoat){:target="_blank"}

<figure>
<img alt="Usando el CTF WebGoat 8.0 para explotar el XXE" class="img img-responsive" src="/resources/images/xxe-goat-ctf.png"/>
<figcaption>
Usando el CTF WebGoat 8.0 para explotar la vulnerabilidad Xml External Entity (XXE)
</figcaption>
</figure>

Primero haremos una petición legitima para ver que formato tendría:

<figure>
<img alt="Haciendo una petición correcta para ver el formato" class="img img-responsive" src="/resources/images/xxe-peticion.png"/>
<figcaption>
Haciendo una petición correcta para ver el formato
</figcaption>
</figure>

Como podemos ver el texto que hemos introducido se incluye en el cuerpo de la petición dentro del tag ```<text>``` y del tag ```<comment>``` 

Si modificamos la petición usando el repeater de Burp y creando una GENERAL EXTERNAL entity (sin olvidarnos de usar los tags validos) que referencia a la raíz del sistema de archivos como nos pide WebGoat obtenemos:

<figure>
<img alt="XXE ejecutado con éxito" class="img img-responsive" src="/resources/images/xxe-resultado.png"/>
<figcaption>
XXE ejecutado con éxito
</figcaption>
</figure>

En una maquina que tuviera un XXE y no estuviera especialmente preparada para ello como WebGoat podríamos leer cualquier archivo con los permisos del usuario que ejecuta el parser (normalmente los del servidor web) por ejemplo /etc/passwd. En el caso de WebGoat solo podemos leer la raíz del sistema de ficheros ```"file:///"```. 

Por ejemplo, el payload para extraer el fichero /etc/password seria asi:

{% highlight xml linenos %}

         <?xml version="1.0"?>
            <!DOCTYPE data [
             <!ELEMENT data (#ANY)>
                <!ENTITY file SYSTEM "file:///etc/passwd">
                        ]>
                <data>&file;</data>

{% endhighlight %}

También podríamos usarlo en sistemas windows:

{% highlight xml linenos %}

        <?xml version="1.0" encoding="ISO-8859-1"?>
        <!DOCTYPE foo [  
        <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "file:///c:/boot.ini" >]><foo>&xxe;</foo>

{% endhighlight %}


Puedes encontrar más payloads [aquí](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20injection){:target="_blank"}


Hasta aquí, este post, seguiré avanzando más sobre XXE en el proximo de la serie.

En este post ha colaborado un amigo pentester llamado Rafa Marti.