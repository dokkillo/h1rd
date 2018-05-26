---
layout: post
title: Chuleta para NMAP
category: Hacking
comments: true
description: Nmap es una de las aplicaciones más importantes de un pentester o hacker etico, pero tambien es una de aplicación de consola con multitud de comandos y opciones, y no viene de más tener una chuleta con los comandos de Nmap más importantes.

tags:   

    - pentesting
    - nmap

---

Nmap es una de las aplicaciones más importantes de un pentester o hacker etico, pero tambien es una de aplicación de consola con multitud de comandos y opciones, y no viene de más tener una chuleta con los comandos de Nmap más importantes.

## Nmap Mapeo de red

Estos escaneos son por defecto, solo escanearan 1000 puertos TCP.

* Escanear una simple IP	_nmap 192.168.1.1_
* Escanear una url	_nmap www.dominioweb.com_
* Escanear un rango de IPs	_nmap 192.168.1.1-20_
* Escanear una red	_nmap 192.168.1.0/24_
* Escanear una red sin escanear los puertos	_nmap -sn 192.168.1.0/24_
* Escanear una red sin dns request haciendo que el scan sea más rapido _nmap -n 192.168.1.0/24_
* Escanear todas las ips de un fichero de texto	_nmap -iL list-of-ips.txt_


## Nmap Detección de puertos

* Escanear un simple puerto _nmap -p 22 192.168.1.1_
* Escanear un rango de puertos	_nmap -p 1-100 192.168.1.1_
* Escanear los 100 puertos más comunes	_nmap -F 192.168.1.1_
* Escanear los 65535 puertos	_nmap -p- 192.168.1.1_
* Escanear un puerto TCP y otro UDP _nmap -p U:25,T:80 192.168.128.1_

## Nmap tipos de escaneo de puertos

* Escanear usando TCP Connect _nmap -sT 192.168.1.1_
* Escanear usando TCP SYN scan _nmap -sS 192.168.1.1_
* Escanear puertos UDP 	_nmap -sU -p 123,161,162 192.168.1.1_
* Escanear usando ACK scan, ideal para detectar firewalls _nmap -sA 192.168.1.1_
* Escanear usando NULL scan  _nmap -sN 192.168.1.1_
* Escanear usando FIN scan  _nmap -sF 192.168.1.1_
* Escanear usando XMAS scan  _nmap -sX 192.168.1.1_

## Detección de sistemas operativos y servicios

* Detectar OS y servicios	_nmap -A 192.168.1.1_
* Detectar servicios	_nmap -sV 192.168.1.1_
* Detección de servicios, mucho más agresiva 	_nmap -sV --version-intensity 5 192.168.1.1_
* Detección de servicios, menos agresiva _nmap -sV --version-intensity 0 192.168.1.1_

## Exportando datos

* Guardar resultado de nmap por defecto _nmap -oN fichero.txt 192.168.1.1_
* Guardar resultado en xml	_nmap -oX fichero.xml 192.168.1.1_
* Guardar resultados en formato grep _nmap -oG outputfile.txt 192.168.1.1_
* Guardar resultados en todos los formatos _nmap -oA outputfile 192.168.1.1_

## Scripts de NMAP

* Usando todos los scripts de nmap seguros _nmap -sV -sC 192.168.1.1_
* Recibiendo ayuda de un script en particular _nmap --script-help=ssl-heartbleed_
* Escaneando con un grupo de scripts _nmap -sV --script=smb* 192.168.1.1_

## Scripts de NMAP HTTP

* Conseguir los titulos de una pagina _nmap --script=http-title 192.168.1.0/24_
* Conseguir los HTTP Headers de webservices _nmap --script=http-headers 192.168.1.0/24_
* Conseguir webs _nmap --script=http-enum 192.168.1.0/24_
