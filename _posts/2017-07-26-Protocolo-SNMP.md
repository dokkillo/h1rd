---
layout: post
title: Protocolo SNMP
category: Redes
comments: true
description: El protocolo SNMP (Simple Network Managment Protocol), trabaja en la capa de aplicación y nos permite trabajar con diferentes dispositivos como routers, switches, firewalls incluso servers, es un protocolo usado para facilitar la información de administracion entre dispositivos de red. 
tags:   
    - protocolos 
---

El protocolo SNMP (Simple Network Managment Protocol), trabaja en la capa de aplicación y nos permite trabajar con diferentes dispositivos como routers, switches, firewalls inclus servers, es un protocolo usado para administrar dispositivos. SNMP nos ayuda a saber si una CPU esta sobrecargada en un determinado router etc. 

<figure>
<img alt="Protocolo SNMP" src="/resources/images/protocolo-snmp.jpg"/>
<figcaption>
El protocolo SNMP facilita la vida a los administradores de red
</figcaption>
</figure>

Hay varias versiones del protocolo SNMP donde se ha mejorado muchisimo la seguridad desde la primera version donde la seguridad era nula.

* Versión 1:  Es una versión bastante simple y basica del protocolo, y extremadamente vulnerable a la enumeración, 

* Versión 2: Es igual que la versión 1, pero con algunas mejoras, todavia era bastante insegura, sobre todo debido a que los dos canales de comunicación, usa dos tipos de password, uno de acceso lectura, y otro de acceso lectura-escritura, por defecto estos passwords son los siguientes, para el acceso de solo lectura: usuario Public password public, y para el acceso de lectura-escritura el usuario es Private y el password es private.

* Versión 3: Esta es la ultima versión del protocolo SNMP, y por fin se mejoro la seguridad, ya que tiene restricción de usuarios, los datos se encriptan, ya no pasan por la red en texto plano pero al ser más complejo de configurar se pueden generar problemas de seguridad por malas configuraciones, como por ejemplo dejar activas las versiones 1 y 2 de SNMP.

# MIBs

Los MIBs o Managment Information Base, es una base de datos virtual que contiene las descripciones de todos los objetos de la red, esta organizada de manera jerarquica e identifica a cada objeto con OIDs, Object Identifier. SNMP se ocupa de convertir el OIDs a un texto entendible por el administrador.




