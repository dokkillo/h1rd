---
layout: post
title: Enumeración de subdominios web
category: Hacking
comments: true
description: Una de las partes más importantes del pentesting es la enumeración, en la que recabaremos toda la información necesaria para que después en las siguientes fases poder atacar al objetivo. En la la parte de la enumeración web se centra en los subdominios, es necesario saber encontrarlos para poder ver que posibles vectores de ataque usar.  En este articulo hablare de varias opciones para extraer todos los subdominios posibles de una web.
tags:   
    - hacker
    - owasp
    - subdominios
    - recon-ng

---

Una de las partes más importantes del pentesting es la enumeración, en la que recabaremos toda la información necesaria para que después en las siguientes fases poder atacar al objetivo. En la la parte de la enumeración web se centra en los subdominios, es necesario saber encontrarlos para poder ver que posibles vectores de ataque usar.  En este articulo hablare de varias opciones para extraer todos los subdominios posibles de una web.

<figure>
<img alt="Enumerando dominios con recon-ng" src="/resources/images/recon-ng-inicio.png"/>
<figcaption>
Enumerando dominios con Recon-ng
</figcaption>
</figure>



## Usando el script EnumAll

Una de las mejores maneras que he visto para enumerar subdominios es usar el script EnumAll creado por @jhaddix y @leifdreizler que usando Recon-ng (Podeis ver varios articulos sobre ello en [Articulos de Recon-ng](http://www.h1rd.com/tags/recon-ng.html){:target="_blank"}) han creado un script que ayuda a recoger mediante ataque de diccionario todos los posibles subdominios existentes.

Para usar este script es necesario:

* Instalar Recon-ng:

{% highlight sql linenos %}

git clone https://LaNMaSteR53@bitbucket.org/LaNMaSteR53/recon-ng.git
cd recon-ng
pip install -r REQUIREMENTS

{% endhighlight %}

* Descargar el fichero de Enumall.py que encontraras en el [repositorio de Jhaddix](https://github.com/jhaddix/domain){:target="_blank"} y ponlo en la carpeta de recon-ng anterior

* Descargar un diccionario completo con subdominos para el ataque, recomiendo [SecList](https://github.com/danielmiessler/SecLists/blob/master/Discovery/DNS/sortedcombied-knock-dnsrecon-fierce-reconng.txt){:target="_blank"}

* Usar el script enumall

{% highlight sql linenos %}

python enumall nombre-dominio -w path-diccionario

{% endhighlight %}

## Buscando en internet

No esta de más buscar subdominios en varias aplicaciones web, como por ejemplo [Pentestertools](https://pentest-tools.com/information-gathering/find-subdomains-of-domain){:target="_blank"} pero si la web es en https, recomiendo buscar en [crt.sh](https://crt.sh/){:target="_blank"} ya que con esta web se pueden hacer consultas por dominios a traves de los certificados de seguridad, ha sido con esta web con la que he encontrado los subdominios más interesantes.




