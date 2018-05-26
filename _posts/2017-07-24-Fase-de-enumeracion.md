---
layout: post
title: Fase de enumeración
category: Hacking
comments: true
description: El objetivo de esta etapa es la obtencion de datos referentes a los usuarios, nombres de equipos, servicios de red etc. Aqui empezamos a realizar conexiones activas en el sistema y consultas dentro del mismo, pero no se realizaran ataques.

tags:   

    - pentesting

---

El objetivo de esta etapa es la obtencion de datos referentes a los usuarios, nombres de equipos, servicios de red etc. Aqui empezamos a realizar conexiones activas en el sistema y consultas dentro del mismo, pero no se realizaran ataques.


## Tecnicas de enumeración

Existen diferentes tecnicas de enumeración a través de las cuales podemos conseguir la información que necesitamos, estas son las seis más conocidas:

* Tarjetas de visita

Por ejemplo las tarjetas de visita vienen con email, el nombre de ese email por ejemplo pepe-perez@evilcorp.com, en un 90% de los casos no estara diciendo que hay un usuario en el sistema llamado pepe-perez.

* Grupos de Windows

Teniendo usuarios, se puede ir consultando a los grupos de windows, si ese usuario pertenece a tal o cual grupo, y asi es posible conocer los usuarios que estan contenidos en cada grupo.

* Zonas de transferencia DNS

Los DNS asocian los _name records_ a una ip y lo guardan en una base de datos, si se le puede engañar al DNS haciendole que te envie una copia de la información de la zona,  teniendo asi acceso a todas las ips relacionadas con el DNS, ftps, servidores etc..

* Fuerza Bruta contra Active Diretory

Active Directory y sus politicas de password, aunque estas tengan la complejidad que la politica de password pide, en el fondo pueden ser passwords simples y debiles como Nombrecompañia + año o Verano2015 etc..

* Passwords por defecto

En las instalaciones tanto de servidores, routers, cms, se dejan muchos passwords por defecto.

* SNMP (Simple Network Managment Protocol)

Es un protocolo de capa de presentación que facilita el intercambio de informacion de administración entre dispositivos de red. El problema de este protocolo es el metodo de autentificación es bastante debil, además que muchas veces estan mal configurado y olvidado.


## Puertos interesantes para la enumeración

* Zonas de transferencia DNS TCP 53
* SMTP o Simple Mail Transfer Protocol TCP 25
* MS RPC Endpoint  TCP 135
* Global Catalog Services, servicio relacionado con Active Directory  TCP/UDP 3368
* NetBIOS, Naming Service TCP 137
* LDAP protocolo usuado por Active Directory TCP/UDP 389
* SMB (Server Message Block) sobre NetBIOS TCP 139
* SNMP (Simple Network protocol) UDP 161
* SMB sobre TCP 445


En los proximos articulos relacionados con enumeración ire escribiendo diferentes tecnicas de enumeración sobre cada protocolo (Netbios, SNMP, LDAP, NTP, SMTP, DNS...)

