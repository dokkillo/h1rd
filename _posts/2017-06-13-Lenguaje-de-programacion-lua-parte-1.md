---
layout: post
title: Lenguaje de programación Lua Parte 1
category: Programacion
comments: true
description: Lua es un lenguaje de programación bastante ligero. Fue creado en 1993 por un grupo de universitarios de Rio de Janeiro. Es un lenguaje bastante interesante de aprender ya que Wireshark y Nmap usan Lua como lenguaje para sus scripts. Fue creado para ofrecer una tecnologia extensible,fue sobre todo para integrarse con C, tiene una sintaxis sencilla, es eficiente y portable.

tags:   
    - programacion
    - lua
---

Lua es un lenguaje de programación bastante ligero. Fue creado en 1993 por un grupo de universitarios de Rio de Janeiro. Es un lenguaje bastante interesante de aprender ya que Wireshark y Nmap usan Lua como lenguaje para sus scripts. Fue creado para ofrecer una tecnologia extensible,fue sobre todo para integrarse con C, tiene una sintaxis sencilla, es eficiente y portable.
La pagina web del proyecto es [Lua.org](https://www.lua.org/){:target="_blank"} alli podras ver como descargarte Lua, funciona tanto en Windows, Linux o Mac.


##Cualidades interesantes

* Es un lenguaje de script muy rapido
* Puede correr en cualquier lado donde haya un compilador de C
* Meta focused
* Pequeño, solo 20k lineas de codigo en C.
* Gratuito

## Tipos de variables en Lua

Hay 8 basicos:

* nil: es parecido a Null 
* boolean: igual que en otros muchos lenguajes, puede ser verdadero o falso, true o false.
* number: en Lua todos los numeros son double, numeros reales con decimales.
* string: igual que en otros muchos lenguajes, son una secuencia de caracteres, y es inmutable, cada vez que se cambia un string, se crea un nuevo con el nuevo valor.
* userdata: este tipo permite guardar codigo en C dentro de variables de Lua.
* function: en Lua, las funciones son variables.
* thread: tipo especial en Lua para la programación en multithreading.
* table: este tipo especial de lua, implementa arrays asociativos que permite almacenar cualquier tipo de datos de Lua excepto nil.

## Asignación de variables en Lua

Igual que pasa en python la asignación de variables es dinamica. En el ejemplo de abajo un ejemplo basico de un Hello World.

<div class="env-header">Hello World en Lua.</div>
{% highlight lua linenos %}

msg = "hello world"
print(msg)

{% endhighlight %}

Una de las primeras cosas que llama la atención de Lua, es que las variables no inicializadas, al usarse, no lanzan una excepción, simplemente, devuelven el tipo nil.

<div class="env-header">Print de una variable no inicializada en Lua.</div>
{% highlight lua linenos %}

print(message)

{% endhighlight %}

<div class="info alert">
    Por cierto, los comentarios en lua son mediante dos guiones \-\- 
</div>

## Operadores

Como en muchos lenguajes de programación, en Lua los operadores son bastante similares, en casi todos, tiene sus cosas especiales.

* Aritmeticos (+, -, *, /...)
* Relacionales (< , >, <=,=>,== y ~= que es diferente en Lua)
* Logicos (and, not, or)
* Unir Strings, en Lua es mediante .. ejemplo "Hola" .. "Mundo"
* Para saber la longuitud de un string o de un array, seria asi #frase

<div class="info alert">
Para sacar la virgulilla de la eñe o ~  en windows es alt + 126 del teclado numerico, en linux es ALTGR + Ñ
</div>

## If / Then / Else en Lua

Como en otros lenguajes de programación, Lua logicamente tiene un If/else/then,

<div class="env-header">Ejemplo de If/else/then  en Lua.</div>
{% highlight lua linenos %}

   if answer < number then
         print "too low"
   elseif answer > number then
        print "too high"
   else
        print "perfect"
   end

{% endhighlight %}

## Bucles en Lua

En Lua hay 4 bucles, muy parecidos al resto de lenguajes de programación.

* while, igual que los while en c#, primero comprueba la condicion, si esta es correcta, sigue si es falsa termina,

<div class="env-header">Ejemplo de while en Lua.</div>
{% highlight lua linenos %}

  local i = 1
    while i<10 do
      print(a[i])
      i = i + 1
    end

{% endhighlight %}


* repeat .. until, es un inverso a while, algo parecido a un do..while, se ejecuta al menos una vez.

<div class="env-header">Ejemplo de repeat .. until en Lua.</div>
{% highlight lua linenos %}

  repeat
      line = os.read()
  until line ~= ""
  print(line)

{% endhighlight %}


* for (numerico), es algo parecido a un for en c# o en java. En el ejemplo siguiente, es un for que imprimira 10 veces el valor i.

<div class="env-header">Ejemplo de for (numerico) en Lua.</div>
{% highlight lua linenos %}

 for i =1,10 do print(i) end

{% endhighlight %}

* for (generico) es parecido a un foreach.

<div class="env-header">Ejemplo de for (generico) en Lua.</div>
{% highlight lua linenos %}

 for i,v in ipairs(a) do print(v) end

{% endhighlight %}

<div class="info alert">
Siempre se puede salir de un loop con un break.
</div>

## Scope en Lua

En Lua, por defecto todas las variables son globales, esto puede llegar a ser bastante horrible, por lo que para que una variable sea local, es decir solo exista dentro de un for, o una funcion es recomendable usar la key __local__ 

<div class="env-header">Ejemplo de variable local en Lua.</div>
{% highlight lua linenos %}

 local name = "h1rd"

{% endhighlight %}

## Proximamente

Para seguir con el curso, el proximo articulo sera sobre funciones en Lua