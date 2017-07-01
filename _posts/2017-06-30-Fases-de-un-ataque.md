---
layout: post
title: Fases de un test de penetración
category: Hacking
comments: true
description: Un test de penetracion consiste en hacer pruebas ofensivas contra mecanismos de defensa del entorno que vamos a analizar, en otras palabras, es hacer de lo que haria un hacker delicuente en ese entorno, una red, una web o ambas, y mediante nuestro trabajo poder avisar a la empresa que arregle esos fallos.Este test se compone en cinco fases, fase de reconocimiento, fase de escaneo, fase de enumeracion, fase de acceso y fase de mantenimiento de acceso.

tags:   
    - hacker
    - pentesting
---

Un test de penetracion consiste en hacer pruebas ofensivas contra mecanismos de defensa del entorno que vamos a analizar, en otras palabras, es hacer de lo que haria un hacker delicuente en ese entorno, una red, una web o ambas, y mediante nuestro trabajo poder avisar a la empresa que arregle esos fallos.
Este test se compone en cinco fases, fase de reconocimiento, fase de escaneo, fase de enumeracion, fase de acceso y fase de mantenimiento de acceso.

## Fase de Reconocimiento

Esta fase consiste en recopilar toda la información posible de nuestro objetivo, que seguramente la necesitaremos más adelante. Esta información consiste en ips, nombres de usuario, trabajadores de la empresa, tipologias de red, tecnologias usadas, emails.

## Fase de escaneo

Con toda la información obtenida previamente se buscan posibles vectores de ataque, aqui hablamos ya de escanear puertos y servicios. Aqui tambien incluimos escaneo de vulnerabilidades que nos ayudara a definir los vectores de ataque.

## Fase de enumeración

El objetivo de esta etapa es la obtenicon de datos referentes a los usuarios, nombres de equipos, servicios de red etc. Aqui empezamos a realizar conexiones activas en el sistema y consultas dentro del mismo.

## Fase de acceso

En esta fase se realiza el acceso al sistema. esta tarea se logra a partir de la explotacion de las vulnerabilidades detectadas por el auditor para comprometer el sistema.

## Fase de mantenimiento de acceso

Esta fase consiste en mantener un acceso al sistema perdurable en el tiempo, y desde alli poder avanzar dentro de la red, es decir, puede que en nuestra intrusion hayamos conseguido entrar en el cutre ordenador del becario pero aque a traves de este ordenador podamos pivotar y acceder al servidor central donde se alojan todos los datos de contabilidad.

Mi idea respecto a este post, es igual que en OWASP, escribir uno o varios articulos de cada fase, e ir poniendo aqui los enlaces.



