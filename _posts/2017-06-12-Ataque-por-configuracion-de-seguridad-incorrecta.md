---
layout: post
title: Ataque por configuracion de seguridad incorrecta
category: Hacking
comments: true
description: Todas las configuraciones relacionadas con la seguridad de una aplicación deben ser definidas, implementadas y mantenidas, ya que las configuraciones por defecto no suelen ser correctas. Ademas se debe mantener todo el codigo actualizado incluido las librerias de terceros que se usen en la aplicación. Esto incluye, cuentas de usuario por defecto, paginas sin usar, acceso a ficheros y directorios desprotegidos, fallos no arreglados, configuraciones incorrectas, que nos den acceso al sistema o a informacion relevante del sistema.

tags:   

    - owasp
---

Todas las configuraciones relacionadas con la seguridad de una aplicación deben ser definidas, implementadas y mantenidas, ya que las configuraciones por defecto no suelen ser correctas. Ademas se debe mantener todo el codigo actualizado incluido las librerias de terceros que se usen en la aplicación.
Esto incluye, cuentas de usuario por defecto, paginas sin usar, acceso a ficheros y directorios desprotegidos, fallos no arreglados, configuraciones incorrectas, que nos den acceso al sistema o a informacion relevante del sistema.

Según la Open Web Application Security Project (Owasp), el ataque por configuracion de seguridad incorrecta forma parte de su [top diez](https://www.owasp.org/index.php/Top_10_2013-A5-Security_Misconfiguration){:target="_blank"}. 

## Configuraciones de seguridad incorrectas y habituales de aplicaciones web.

* Mostrar codigo de la aplicación al usuario cuando se genera un error en la aplicación.
* Configuración incorrecta de la gestión de logs, por ejemplo elmah.axd o trace.axd, por defecto sus logs son visibles a todo el mundo...
* Paquetes de terceros sin actualizar.
* y muchos más, la mejor manera para darse cuenta de la gravedad de este problema es viendo la posibilidad de encontrar estos problemas desde google, incluso, solo accediendo a [Google Hacking DB](https://www.exploit-db.com/google-hacking-database/){:target="_blank"}.

