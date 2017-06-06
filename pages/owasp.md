---
layout: page
title: OWASP
description: Top Ten OWASP
---

OWASP (Open Web Application Security Project) es una fundación dedicada a seleccionar y combatir las causas por las que el software es inseguro. Ha publicado una lista de los riesgos de seguridad más importantes de las aplicaciones web. 

<figure>
<img alt="OWASP" src="/resources/images/owasp.png"/>
<figcaption>
OWASP 
</figcaption>
</figure>

## 1. Inyeccion

SQL injection o inyeccion de SQL es una vulnerabilidad donde el atacante puede modificar una query correcta y cambiar asi el funcionamiento de la web. Puede haber inyecciones de otros tipos como (LDAP, XPath, nosql, os....)

En estos articulos hable sobre la inyeccion de sql:

* [Que es la Inyección de SQL]({% post_url 2017-05-15-que-es-sql-injection %}) 
* [Tipos de SQL injection]({% post_url 2017-05-16-tipos-de-sql-injection %}) 
* [SQL injection por error]({% post_url 2017-05-18-sql-injection-por-error %})
* [SQL injection por unión]({% post_url 2017-05-21-sql-injection-por-union %})
* [SQL injection ciego si o no]({% post_url 2017-05-22-sql-injection-ciego-sino %})
* [SQL injection ciego por tiempo]({% post_url 2017-05-23-sql-injection-ciego-tiempo %})


## 2. Pérdida de Autentificación y Gestión de sesiones

Session Hijacking, forma parte de la perdida de Autenticación y gestión de sesiones, esta reconocida como la segunda vulnerabilidad web más peligrosa según la Open Web Application Security Project (OWASP) despues de Injection. Esta vulnerabilidad permite a un atacante acceder a una aplicación como si fuese otro usuario real.
Hay varios tipos de vectores de ataque para conseguir explotar esta vulnerabiliad, por ejemplo por Cross-site scripting mala configuracion de logs, problemas de sniffing.  En estas semanas ire publicando post sobre cada uno de ellos y completando esta información.

En este articulo hablo del secuestro de sesion:

* [Que es session hijacking]({% post_url 2017-05-26-que-es-session-hijacking %}) 


## 3. Cross Site Scripting (XSS)

Esta vulnerabilidad consiste en que un atacante es capaz de inyectar codigo javascript en una pagina visitada por el usuario y poder secuestrar la sesion del usuario o comprometer su navegador web.

Estos articulos hablo del Cross site scripting:

* [Entendiendo el vector de ataque XSS]({% post_url 2017-05-31-Entendiendo-el-vector-de-ataque-xss %}) 
* [Ataque XSS Reflejado]({% post_url 2017-05-31-Ataque-xss-reflejado %}) 
* [Ataque XSS Persistido]({% post_url 2017-06-01-Ataque-xss-persistido %}) 
* [Ataque XSS a un formulario solo con validación cliente]({% post_url 2017-06-03-Ataque-xss-formularios-validacion-cliente %}) 



## 4. Referencia directa insegura de objetos

## 5. Configuración de seguridad incorrecta

## 6. Exposición de datos sensibles

## 7. Ausencia de control de acceso en funciones

## 8. Falsificacion de peticiones en sitios cruzados (CSRF)

El ataque por CSRF o XSRF, consiste en forzar al usuario a ejecutar peticiones no deseadas en una web, en la que estan autentificados, si que este se de cuenta. En este tipo de ataque es necesaria la utilización de ingenieria social para engañar a la victima y que ejecute la petición falsa, sea mediante un email, o un link de una red social.

*  [Ataque por Cross Site Request Forgery]({% post_url 2017-06-06-Ataque-Cross-Site-Request-Forgery-CSRF %}) 


## 9. Utilización de componentes con vulnerabilidades conocidas

## 10. Redirecciones y reenvios no validos

