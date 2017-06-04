---
layout: post
title: Cabecera HTTP
category: Redes
comments: true
description: Las cabeceras HTTP son los metadatos que se envian en las peticiones HTTP para proporcionar información esencial sobre la transacción en curso. La mejor manera de entender HTTP es creando peticiones a mano y ver que va sucediendo.
tags:
    - protocolos
    - intro
    - HTTP
    - telnet
---

Las cabeceras HTTP son los metadatos que se envian en las peticiones HTTP para proporcionar información esencial sobre la transacción en curso. La mejor manera de entender HTTP es creando peticiones a mano y ver que va sucediendo.

## Telnet

Para poder crear las peticiones a mano, lo mejor es usar el programa de Telnet, si ese que se usaba en los 80 para acceder a las BBS (Los foros de esa epoca..), se dejo de usar porque enviaba todos los datos en forma plana. Tanto en Windows como en linux, tenemos una aplicacion llamada Telnet que podemos acceder a ella desde una consola o desde cmd.

## Creando las peticiones HTTP a mano

Para estas pruebas practicare con una pagina web llamada picandocodigo.net, para ello abrimos telnet con la terminal y escribimos:

{% highlight html linenos %}

telnet picandocodigo.net 80

{% endhighlight %}

Telnet funciona con el puerto 23 por defecto, por lo que tenemos que decirle que se conecte a la web por el puerto 80. Al ejecutar el comando anterior recibimos esta respuesta:

{% highlight html linenos %}

Trying 192.185.21.193...
Connected to picandocodigo.net.
Escape character is '^]'.


{% endhighlight %}

Por lo que ahora nosotros escribimos nuestra petición:


{% highlight html linenos %}

GET / HTTP/1.1
Host: www.picandocodigo.net

{% endhighlight %}

En ella usamos el verbo GET, y pedimos / es decir la raiz de la web mediante HTTP/1.1 y del host www.picandocodigo.net, esta es la minima cabecera necesaria para ejecutar una peticion correcta.
La respuesta que recibimos es la siguiente:

{% highlight html linenos %}

HTTP/1.1 301 Moved Permanently
Server: nginx/1.12.0
Date: Tue, 30 May 2017 05:16:51 GMT
Content-Type: text/html; charset=UTF-8
Content-Length: 0
Connection: keep-alive
Location: http://picandocodigo.net/

{% endhighlight %}

La respuesta que recibimos es un codigo 301, es decir todas las peticiones a www.picandocodigo.net se deben mover a picandocodigo.net, Asi que cambiamos nuestra peticion a la url que nos dicen.

{% highlight html linenos %}

GET / HTTP/1.1
Host: picandocodigo.net

{% endhighlight %}

Y ahora ya recibimos todo el html de la pagina. correctamente.

{% highlight html linenos %}

HTTP/1.1 200 OK
Date: Tue, 30 May 2017 05:16:51 GMT
Content-Type: text/html
Content-Length: 1221

<html>
....
</html>

{% endhighlight %}

Como dije este es la petición HTTP básica, se puede complementar con muchas más caberas según se necesite, tal como hacen los navegadores. Algunas de las más importantes:

* Accept indica el MIME aceptado
* Accept-Charset indica el código de caracteres aceptado
* Accept-Encoding indica el método de compresión aceptado
* Accept-Language indica el idioma aceptado
* User-Agent para describir al navegador o agente que esta haciendo la petición
* Server indica el tipo de servidor
* Allow métodos permitidos para el recurso
* Content-Type indica el MIME del contenido
* Content-Length longitud del mensaje
* Location indica donde está el contenido
* Referer indica el origen de la petición
* Date fecha de creación
* Set-Cookie Cabeceras para control de cookies
* Cookie Cabeceras para control de cookies
* Host indica máquina destino del mensaje
* Connection indica como establecer la conexión

