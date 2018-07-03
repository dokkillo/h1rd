---
layout: post
title: Recon sobre el espacio de direcciones IP
category: Hacking
comments: true
description: La fase de reconocimiento, probablemente sea una de las fases más importantes de un pentesting o bug hunting, en esta fase es necesario recopilar toda la información posible, con ella podremos hacernos una imagen de como esta montada la web, que servicios usa, en que sistema operativo estan etc, Más adelante esa información nos sera muy util. En este articulo nos centraremos en varios recursos web que se pueden usar para descubrir el espacio de direcciones IP de nuestro target. 
tags:   
    - recon
---

La fase de reconocimiento, probablemente sea una de las fases más importantes de un pentesting o bug hunting, en esta fase es necesario recopilar toda la información posible, con ella podremos hacernos una imagen de como esta montada la web, que servicios usa, en que sistema operativo estan etc, Más adelante esa información nos sera muy util. En este articulo nos centraremos en varios recursos web que se pueden usar para descubrir el espacio de direcciones IP de nuestro target. 

## BGP.HE.NET

Esta aplicación web nos permitira buscar información relativa a los DNS y rangos de IPS, tanto de la empresa, ya que podemos buscar por nombre como del dominio.

<figure>
<img alt="Captura de pantalla usando BGP.HE.NET para ver el rango de ips de Github" class="img img-responsive" src="/resources/images/recon-rango-ips.png"/>
<figcaption>
Captura de pantalla usando BGP.HE.NET para ver el rango de ips de Github"
</figcaption>
</figure>

* Enlace : [https://bgp.he.net](https://bgp.he.net/){:target="_blank"}


## WHOIS.ARIN.NET

En esta web podremos encontrar más información sobre IPs y datos de empresa, pero sobre todo de empresas americanas.

* Enlace : [https://whois.arin.net/ui/query.do](https://whois.arin.net/ui/query.do){:target="_blank"}

## APPS.DB.RIPE.NET

Esta web nos puede ayudar a hacer nuestro recon mucho más facil, ya que puede complementar la información que recibamos de WHOIS.ARIN.NET.


* Enlace : [https://apps.db.ripe.net/db-web-ui/#/fulltextsearch](https://apps.db.ripe.net/db-web-ui/#/fulltextsearch){:target="_blank"}

## REVERSE.REPORT




* Enlace : [http://www.reverse.report/](http://www.reverse.report/){:target="_blank"}



