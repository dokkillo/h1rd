---
layout: post
title: Lenguaje de programación Lua Funciones
category: Programacion
comments: true
description: En cualquier lenguaje de programación las funciones son la mejor manera para no repetir codigo, son muy importantes y necesarias. En este post hablaremos de como son las funciones en Lua.

tags:   
    - programacion
    - lua
---

En cualquier lenguaje de programación las funciones son la mejor manera para no repetir codigo, son muy importantes y necesarias. En este post hablaremos de como son las funciones en Lua.

La pagina web del proyecto es [Lua.org](https://www.lua.org/){:target="_blank"} alli podras ver como descargarte Lua, funciona tanto en Windows, Linux o Mac.


## Funciones

Una de las primeras cosas que tenemos que tener en cuenta, es que Lua es un lenguaje de programación interpretado por lo que, antes de usar la funcion, hay que crearla.

{% highlight lua linenos %}

function getRandomNumber(maxvalue)
    math.randomseed(os.time())
    math.random()
    return math.random(maxvalue)
end

{% endhighlight %}

Como puedes ver, no se pasan ni tipos, en los parametros ni en el valor a devolver.


## Funciones variadicas

Lua permite funciones variadicas, son funciones de __aridad__ indefida, es decir, que acepta una cantidad de argumentos variable. Javascript tambien acepta funciones variadicas. 
En la parte de los parametros de una funcion, añadimos __...__ y en el cuerpo asignamos las variables, por ejemplo, en el caso del ejemplo lo asignamos a dos variable, si hubiese mas, la función no las cogera.

En Lua son asi:

{% highlight lua linenos %}

function totalCost(...)
    num1, num2 = ...
    return num1 + num2
end

{% endhighlight %}

Y por ejemplo para usarla, seria algo tan facil como totalCost(100,25).

En este post ha sido una introduccion de como son las funciones en Lua, las funciones normales son bastante parecidas a otros lenguajes, aqui la curiosidad esta en las funciones variadicas. En proximos post me extendere más sobre ellas.
