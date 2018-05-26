---
layout: post
title: Enumeración sobre el protocolo SMTP
category: Hacking
comments: true
description: El protocolo SMTP (Simple Mail Transfer Protocol) se ocupa del intercambio de emails entre diferentes ordenadores u otros dispositivos. Este protocolo tiene algunas limitaciones por lo que se asocia otros protocolos como IMAP o POP, ocupandose SMTP solo del envio y recepción de emails. Lo bueno de este protocolo es que en la fase de enumeración podemos usarlo para averiguar diferentes usuarios de nuestro sistema objetivo, y usarlos posteriormente en diferentes fases.
tags:   

    - protocolos
    - metasploitable2

---

El protocolo SMTP (Simple Mail Transfer Protocol) se ocupa del intercambio de emails entre diferentes ordenadores u otros dispositivos. Este protocolo tiene algunas limitaciones por lo que se asocia otros protocolos como IMAP o POP, ocupandose SMTP solo del envio y recepción de emails. Lo bueno de este protocolo es que en la fase de enumeración podemos usarlo para averiguar diferentes usuarios de nuestro sistema objetivo, y usarlos posteriormente en diferentes fases.


## Protocolo SMTP

El protocolo SMTP es un protocolo orientado a la conexión y basado en texto, en el que emisor del email se comunica con el servidor mediante comandos de texto, aqui una lista de los comandos más importantes.

HELO, para abrir una sesión con el servidor
MAIL FROM, para indicar quien envía el mensaje
RCPT TO, para indicar el destinatario del mensaje
DATA, para indicar el comienzo del mensaje, éste finalizará cuando haya una línea únicamente con un punto.
QUIT, para cerrar la sesión
RSET Aborta la transacción en curso y borra todos los registros.
SEND Inicia una transacción en la cual el mensaje se entrega a una terminal.
SOML El mensaje se entrega a un terminal o a un buzón.
SAML El mensaje se entrega a un terminal y a un buzón.
VRFY Solicita al servidor la verificación de todo un argumento.
EXPN Solicita al servidor la confirmación del argumento.
HELP Permite solicitar información sobre un comando.
NOOP Se emplea para reiniciar los temporizadores.
TURN Solicita al servidor que intercambien los papeles.

El protocolo SMTP suele trabajar en el puerto 25 y el 587 para el modo seguro, aun asi es algo bastante variable ya que se puede configurar para que trabaje en diferentes puertos.

## Usando el protocolo SMTP en la fase enumeración

En la maquina virtual de Metasploitable 2, tenemos el protocolo SMTP activo en el puerto 25, si ejecutamos nmap sobre ella, preguntando sobre que servicio esta usando.

{% highlight sql linenos %}

nmap -sT -sV -sC -T5 -p 25 192.168.1.39

{% endhighlight %}

Recibiremos estos datos:

{% highlight sql linenos %}

Nmap scan report for 192.168.1.39
Host is up (0.00065s latency).

PORT   STATE SERVICE VERSION
25/tcp open  smtp    Postfix smtpd
|_smtp-commands: metasploitable.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, 
|_ssl-date: 2017-08-18T05:50:47+00:00; -1s from scanner time.
| sslv2: 
|   SSLv2 supported
|   ciphers: 
|     SSL2_RC4_128_WITH_MD5
|     SSL2_DES_64_CBC_WITH_MD5
|     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|     SSL2_RC2_128_CBC_WITH_MD5
|_    SSL2_DES_192_EDE3_CBC_WITH_MD5
MAC Address: 00:0C:29:D3:5F:CD (VMware)
Service Info: Host:  metasploitable.localdomain

Host script results:
|_clock-skew: mean: -1s, deviation: 0s, median: -1s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.72 seconds


{% endhighlight %}

Por ahora, lo que nos interesa es el comando VRFY, que nos permite saber si un usuario existe, esta activo.

Ahora usaremos una aplicación instalada en Kali, llamada smtp-user-enum, donde mediante un diccionario (usaremos el predefinido por Kali) podremos comprobar si existen estos usuarios.

{% highlight sql linenos %}

smtp-user-enum -M VRFY -U /usr/share/metasploit-framework/data/wordlists/namelist.txt -t 192.168.1.39

{% endhighlight %}


Y en unos segundos... sabemos que el sistema tiene los siguientes usuarios:

{% highlight sql linenos %}

Scan started at Mon Aug 21 07:00:50 2017 #########
192.168.1.39: backup exists
192.168.1.39: dhcp exists
192.168.1.39: ftp exists
192.168.1.39: games exists
192.168.1.39: irc exists
192.168.1.39: mail exists
192.168.1.39: mysql exists
192.168.1.39: news exists
192.168.1.39: proxy exists
192.168.1.39: root exists
192.168.1.39: service exists
192.168.1.39: snmp exists
192.168.1.39: syslog exists
192.168.1.39: user exists
Scan completed at Mon Aug 21 07:00:54 2017 #########
14 results.

{% endhighlight %}


<figure>
<img alt="Usando el programa smtp-user-enum en Kali Linux" src="/resources/images/smtp-enum.png"/>
<figcaption>
Usando el programa smtp-user-enum en Kali Linux
</figcaption>
</figure>

