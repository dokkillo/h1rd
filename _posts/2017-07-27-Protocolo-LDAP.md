---
layout: post
title: Protocolo LDAP
category: Redes
comments: true
description: El protocolo LDAP (Ligthweight Directory Access Protocol) es un protocolo a nivel de aplicación que permite el acceso a un servicio directorio ordenado y distribuido para buscar diversa información en un entorno de red. LDAP se le considera tambien como una base de datos a la que pueden realizarse consultas.
tags:   
    - protocolos 
---

El protocolo LDAP (Ligthweight Directory Access Protocol) es un protocolo a nivel de aplicación que permite el acceso a un servicio directorio ordenado y distribuido para buscar diversa información en un entorno de red. LDAP se le considera tambien como una base de datos a la que pueden realizarse consultas.


## Estructura jerarquica de LDAP

Un directorio en LDAP es un conjunto de objetos con atributos organizados de manera logica y jerarquica, es parecido a como se organiza un listin telefonico, que es una serie de nombre, sean personas o empresas, que estan ordenados alfabeticamente, cada nombre tiene una dirección y un numero de telefono. Muchas veces LDAP tambien refleja organizaciones jerarquicas por limites geograficos, politicos u organizacionales, según como se haya elegido. Actualmente en las organizaciones actualmente se organiza LDAP con nombres de DNS (Sistema de nombres de dominio) y asi estructurar los niveles más altos de la organización.

Es decir, un directorio es arbol de entradas, cada entrada tiene un identificador unico, conocido como su *Nombre distinguido* (DN) tiene un conjunto de atributos, cada atributo tiene un nombre y varios valores más.

<figure>
<img alt="Protocolo LDAP" src="/resources/images/ldap.png"/>
<figcaption>
Organización jerarquica del protocolo LDAP
</figcaption>
</figure>

* dc es la entrada especifica por donde empieza el arbol y sus hijos "dc=pisosoftware,dc=com"
* ou unidad organizacional, o el departamento 
* cn nombre común o nombre distinguido relativo
* uid es el id de los cn

## Puertos DSA

* TCP/UDP 389
* LDAPS 636 PARA SSL
* Global catalog, version light de la base de datos De LDAP, Puertos TCP/UDP 3268, 
* La version SSL de Global Catalog es 3269





