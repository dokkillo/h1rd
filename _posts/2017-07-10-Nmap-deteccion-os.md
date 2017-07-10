---
layout: post
title: Nmap detección de OS
category: Hacking
comments: true
description: En NMAP hasta ahora hemos estado centrados en descubrir puertos abiertos, servicios y demas, ahora en este post podremos saber como que versiones o que programas estan corriendo en se puerto, o incluso cual es el sistema operativo del host

tags:   
    - hacker
    - pentesting
    - nmap

---

En NMAP hasta ahora hemos estado centrados en descubrir puertos abiertos, servicios y demas, ahora en este post podremos saber como que versiones o que programas estan corriendo en se puerto, o incluso cual es el sistema operativo del host.


## -sV  

Esto nos ayudara a saber que la version del programa que esta corriendo dentras del puerto abierto, esta opción se puede combianr con --version-intensity que puede ir de 0 a 9, por defecto es 7. Este comando puede hacer que el escaneo vaya muchisimo más lento, una opción correcta seria usar este comando solo en el puerto que nos interesa analizar.

{% highlight sql linenos %}

nmap -sV 192.168.1.1
nmap -sV -p 21 192.168.1.1

{% endhighlight %}



## -O

La detección del sistema operativo del host a analizar se hace mediante la opción -O pero al igual que la detección de versiones tiene un impacto importante en la velocidad del escaneo. Esta opción es mucho más efectiva si encuentra al menos un puerto abierto y un puerto cerrado.
Se recomienda usar con las siguientes opciones:

* --osscan-limit desactiva la deteccion del sistema operativo si no puede encontrar al menos un puerto abierto y otro cerrado
* --osscan-guess, --fuzzy  ambos dos son equivalentes, le dicen al sistema que sea más agresivo al adivinar el sistema operativo de la maquina.
* --max-os-tries 4, por defecto es 5, es para limitar el numero de intentos que hara NMAP para descubrir el sistema operativo del host.



