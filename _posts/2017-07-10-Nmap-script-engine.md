---
layout: post
title: Nmap script engine
category: Hacking
comments: true
description: NMAP tiene un modulo donde podemos ampliar la funcionalidad de NMAP mediante scripts hechos por el usuario, este modulo es Scripting Engine o NSE.Cada dia de hoy hay 572 scripts en la libreria por defecto de NSE y cada dia se añaden más.

tags:   


    - nmap

---

NMAP tiene un modulo donde podemos ampliar la funcionalidad de NMAP mediante scripts hechos por el usuario, este modulo es Scripting Engine o NSE.
A dia de hoy hay 572 scripts en la libreria por defecto de NSE y cada dia se añaden más. Puedes ver la [lista de los scripts de NMAP](https://nmap.org/nsedoc/){:target="_blank"}

NSE se construyo para ampliar NMAP en cinco areas diferentes:

* Detección de versiones
* Escaneo de redes
* Deteccion de vulnerabilidades
* Detección de backdoors
* Explotación de vulnerabilidades


## Usando Nmap Script Engine

Para usar el modulo de scripts es necesario usar la opcion -sC, esto ejecutara __todos__ los scripts, con los problemas asociados de velocidad, otra opcion más interesante puede ser ejecutar los scripts necesarios mediante ---script. Es posible ejecutar un script en particular o una categoria en particular.

El NSE tiene las siguientes categorias:

* auth
* discovery
* fuzzer
* safe
* broadcast
* dos
* intrusive
* version
* brute
* exploit
* malware
* vuln
* default
* external
* safe


{% highlight sql linenos %}

nmap -sC cnn.com
nmap -p 80 --script http-crono www.cnn.com
nmap -p 80 --script safe cnn.com


{% endhighlight %}


