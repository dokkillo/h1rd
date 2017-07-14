---
layout: post
title: Nmap evadiendo firewalls
category: Hacking
comments: true
description: En el mundo empresarial real, los equipos estan protegidos detrás de firewalls, IDS o NATs. En este post hablaremos de las diferentes maneras que usa NMAP para saltarse esas defensas y seguir haciendo su trabajo.

tags:   
    - hacker
    - pentesting
    - nmap
    - firewall
    - ids

---

En el mundo empresarial real, los equipos estan protegidos detrás de firewalls, NAT, IDS u otras defensas. En este post hablaremos de las diferentes maneras que usa NMAP para saltarse esas defensas y seguir haciendo su trabajo.
Las defensas más habituales que nos encontraremos seran:

* Firewalls
* NAT
* IDS

## Firewalls

Un firewall es un sistema de seguridad que controla el trafico de red que pasa entre dos redes, se ocupa de mirar los paquetes que viajan de una red a otra, permitiendo o denegando basandos en la cabecera del paquete o a veces el contenido de este. Toma las decisiones principalmente basandose en el socket (ip y puerto) y tambien según los flags activos.

Hay tres tipos de firewalls principales:

* Stateless, este firewall se basa en unas reglas, si el paquete a entrar cumple esas reglas, por ejemplo acceso al puerto 80, se le deja pasar, sino no. No inspecciona los flags de los paquetes TCP.
* Statefull, este tipo de firewall se basa en una serie de reglas añadidas por el administrador como el firewall tipo stateless, pero tambien se basa según el estado de la conexion, es decir mantienen una tabla con las conexiones aceptadas y establecidas, por lo que si llega un paquete que no es una conexion establecida con un flag RST o un paquete con NFX, este paquete sera eliminado.
* Proxy, este tipo de firewall se ocupa de interpretar el contenido del paquete y permitirlo o no según sus reglas, si el paquete  es de un contenido que no soporta, el firewall se comporta como si fuera un statefull firewall.


## Como saber que hemos encontrado un firewall

Hay tres opciones que podemos usar con NMAP para deducir que hemos encontrado un firewall, estas son __-traceroute__, __-O__ y __--badsum__ esta opción hace que NMAP cree un checksum incorrecto en la cabecera de TCP, todos los hosts borraran los paquetes, y si hubiese alguna respuesta, esta vendria de un firewall.
Más sobre esta tecnica en [Nmap bad cheksum](https://nmap.org/p60-12.html){:target="_blank"} 

## Maneras para saltarse un firewall: fragmentación

Una manera eficaz de saltarse un firewall es mediante la fragmentacion de los paquetes. La capa fisica impone una restricción en el tamaño maximo del paquete o MTU (Maximun Transmission Unit). Si un paquete tiene 2000 byts de tamaño y el MTU es de 1000 bytes, el paquete debe separarse en dos.
La fragmentación ayuda a evadir firewalls porque volver a unir los paquetes es bastante costoso, y generalmente los firewalls dejan pasar los paquetes. Esto es sobre todo más efectivo cuando elegimos un tamaño de fragmento que separa la cabecera TCP es varios paquetes.

Maneras de hacerlo:

__-f__ trozos de 8 bytes

__-f -f ___ trozos de 16 bytes

__--mtu__ tamaño del trozo elegido por el usuario

{% highlight sql linenos %}

nmap -f -f 192.168.1.1
nmap -mtu 25 192.168.1.1

{% endhighlight %}


## Maneras para saltarse un firewall : idle scan

Este scan se basa en que hay sistemas que aumentan en uno el campo id, cada vez que envian un datagrama fuera, si podemos encontrar un sistema que haga esto, podemos realizar un escaner que esconda completamente nuestra identidad.

Idle scan funciona de esta manera:

* Supon que encontramos una impresora que detectamos que aumenta el campo id en uno, cada vez que envia un datagrama fuera, asi que enviamos un paquete a ese sistema, este nos contesta con un valor id, que nosotros anotamos.

* Ahora enviamos un paquete SYN al objetivo, usando la ip del sistema idle, si el puerto esta abierto, el target contestara al sistema idle. Si no, no lo hara.

* Nosotros volvemos a enviar otro paquete al sistema idle, si en este caso el numero del id que nos contesta, ha aumentado en dos, es que el sistema idle ha recibido un paquete del sistema target notificandole que el puerto estaba abierto, si solo ha aumentado en uno, el puerto estaba cerrado.

Para usar el idle scan:

__-sI zombie host:puerto__ 

Se pueden detectar idle host con el script ipidseq.

{% highlight sql linenos %}

nmap 192.168.1.12 --script ipidseq
nmap 192.168.1.1 -sI 192.168.1.12


{% endhighlight %}

## Otras maneras de ocultarse

Ademas de firewallls, tambien podemos encontrarnos con IDS, sistemas que se ocupan de monitorizar todo el movimiento extraño de la red y guardarlo en logs. Por lo que interesa, sobre todo en pruebas de red team, pasar nuestro trafico de una manera lo más legitima posible.

__-T paranoid__ para reducir la velocidad de escaneo y no llamar la atención.

__-source-port portnum -g portnum__ puerto origen

__--data-length num__ añade datos random.

Por ejemplo, todo junto podemos hacer que nuestro escan parezca que viene de una web segura con un información encriptada.

{% highlight sql linenos %}

nmap -PA -g 443 -p 6756 --data-length 800 192.168.1.12

{% endhighlight %}

__-D ip1, ip2, ME, ip3__ Este Decoy nos permite añadir otras direcciones que pueden ser usadas como decoys










