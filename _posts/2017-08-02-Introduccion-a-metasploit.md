---
layout: post
title: Introducción a Metasploit
category: Hacking
comments: true
description: Metasploit es un framework open source de seguridad creado por H. D. Moore aunque en el 2009 fue comprado por la empresa rapid7, desde entonces tiene varias versiones comerciales ademas de la versión gratuita. Originalmente estaba escrito en Perl pero fue migrado a Ruby.
tags:       

    - pentesting
    - metasploit
---

Metasploit es un framework open source de seguridad creado por H. D. Moore aunque en el 2009 fue comprado por la empresa rapid7, desde entonces tiene varias versiones comerciales ademas de la versión gratuita. Originalmente estaba escrito en Perl pero fue migrado a Ruby.

Como Framework, Metasploit se especializa en ejecutar exploits en redes, sistemas operativos y aplicaciones, y tambien en desarrollar nuevos exploits, además cuenta con Meterpreter que cuando es ejecutado en un sistema remoto ayuda a mantener el acceso a la maquina y a controlarla más facilmente.

## Ejecutar Metasploit

La manera más facil de instalar y usar Metasploit es hacerlo mediante Kali Linux,  ya que viene instalado y configurado de serie, aun asi hay que ejecutar ciertos comandos la primera vez que lo usamos.

Estos son los comandos :

* service postgresql start    Metasploit usa PostgreSQL como base de datos por lo tanto necesita estar ejecutandose antes de lanzarse.
* msfdb init  Con PostgreSql funcionando, hay que iniciar la base de datos de Metasploit
* msfconsole  Es el comando de inicio de Metasploit. Si todo ha ido bien al ejecutar en Metasploit el comando __db_status__ nos dira que estamos conectados a la base de datos de Metasploit.

<figure>
<img alt="Pantalla inicio de Metasploit" src="/resources/images/metasploit-intro.png"/>
<figcaption>
Pantalla de inicio de Metasploit
</figcaption>
</figure>


## Terminologia basica de Metasploit

Para no perdernos, hay ciertos terminos muy usados en Metasploit que deberiamos conocer y saber usar: 

* Interfaces, son metodos con los que interactuaremos con Metasploit, la que más se suele usar es la linea de comandos. Tambien hay una parte grafica conocida como Armitage.
* Utilidades (Utilities) son pequeñas herramientas que proveen información adicional para ayudarnos mientras trabajamos con el framework
* Modulos (Modules) son el corazón de Metasploit, gran parte de la funcionalidad del framework viene a través de los modulos.
* Exploits, son modulos que intentan vulnerar un sistema explotando sus debilidades
* Escaners (Scanners) son tambien modulos, son conocidos como modulos auxiliares y nos pueden ayudar a conseguir más información del sistema.
* Payload, es un fragmento de codigo que se envia al sistema objetivo, para conseguir acceso o para tomer control de este. Un payload puede ser unos simples comandos o sofisticados programas de acceso remoto, tambien pueden hacer que la maquina objetivo se comunique con la maquina del atacante mediante el uso de listeners.

<figure>
<img alt="Arquitectura de Metasploit" class="img img-responsive" src="/resources/images/Metasploit-arquitectura.png"/>
<figcaption>
Arquitectura de Metasploit
</figcaption>
</figure>


## Cambios en Metasploit

Metasploit es un proyecto open source y vivo, y eso significa que suele haber cambios habituales, ya sea para añadir nuevas funcionalidades o para unir funcionalidades parecidas, por ejemplo:

En muchos blogs, tutoriales, videos de youtube, se habla de un comando llamado msfcli, que crea permite al pentester crear un script y automatizar la ejecución del framework, ya no existe, ahora se llama __msfconsole -x__
O tambien msfpayload que permite crear payloads que envias a la maquina objetivo y el comando msfencode que permite alterar la firma de los payloads haciendolos más indetectables a los antivirus, se unieron en un nuevo comando llamado __msfvenom__
Es bueno saberlo, ya que cuando esos tutoriales o articulos hablen de estos comandos seguramente con cambiar solo el comando principal el resto funcione correctamente.



## Comandos basicos de Metasploit

Durante el uso de Metasploit hay ciertos comandos que en Metasploit que usaremos muchos, generalmente seran estos:

* msfconsole para iniciar la aplicacion en terminal
* search para buscar dentro de la base de datos de Metaploit, por ejemplo search nmap
* use  cuando ya sabemos que exploit usaremos en Metasploit escribiriamos por ejemplo use  exploit/multi/misc/legend_bot_exec   
* show options ya dentro del exploit ejecutamos este comando para saber que parametros hay que completar antes de ejecutarlo.
* info con el comando info podremos tener toda la información sobre que hace este exploit
* set or setg  para introducir los campos requeridos que necesitamos para ejecutar el exploit, set RHOST 192.168.1.35
* unset para quitar un campo ya introducido
* run  ejecutamos el exploit
* help ayuda general de Metasploit


## Enlances utiles para aprender Metasploit

* [Curso gratuito de Offensive Security sobre Metasploit](https://www.offensive-security.com/metasploit-unleashed/){:target="_blank"}
* [Pagina oficial de Metasploit](https://www.rapid7.com/products/metasploit/){:target="_blank"}
* [Github de Metasploit](https://github.com/rapid7/metasploit-framework){:target="_blank"}






