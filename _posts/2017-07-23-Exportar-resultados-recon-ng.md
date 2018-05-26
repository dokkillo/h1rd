---
layout: post
title: Exportar resultados con Recon-ng
category: Hacking
comments: true
description: Cuando ya hemos conseguido con Recon-ng todos los datos que necesitabamos, llega el momento de exportar todos los datos en ficheros que podamos manejar posteriormente. En Recon-ng se puede extraer los datos en diferentes tipos de ficheros. 
tags:   


    - recon-ng

---

Cuando ya hemos conseguido con Recon-ng todos los datos que necesitabamos, llega el momento de exportar todos los datos en ficheros que podamos manejar posteriormente. En Recon-ng se puede extraer los datos en diferentes tipos de ficheros. 

## Formato CSV

Para extraer nuestra información en formato csv, es necesario usar el modulo _reporting/csv_ , por defecto extraera informacion de la tabla Host, si queremos extraer información de otras tablas, seria necesario escribir SET table nombreTabla, por ejemplo contacts.
Tambien es posible cambiar la ruta en donde se guardara el fichero cambiando el valor de la variable FILENAME.

{% highlight sql linenos %}

[recon-ng][default] > use reporting/csv
[recon-ng][default] > show info

{% endhighlight %}

## Formato HTML

Con el modulo _reporting/html_ se genera una pagina html donde se vuelca toda la información de las tablas. En este modulo nos pide que completemos tres variables,
CREATOR, el nombre de quien ha creado este reporte, ira en el footer del html. CUSTOMER, la empresa a la que hemos hecho OSINT, ira en el header del html, y SANITIZE si queremos o no enmascarar los datos personales que hemos conseguido.

{% highlight sql linenos %}

[recon-ng][default] > use reporting/html
[recon-ng][default] > show info

{% endhighlight %}

## Formato JSON

Con el modulo _reporting/json_ se genera un fichero json donde podemos exportar la información que queremos, al contrario que en el formato csv, aqui podemos seleccionar más de una tabla a la vez, mediante la variable TABLES, donde añadimos las tablas que queremos separadas por una coma.

{% highlight sql linenos %}

[recon-ng][default] > use reporting/json
[recon-ng][default] > show info

{% endhighlight %}

## Formato TXT

Usando el modulo _reporting/list_ podemos exportar los valores de una tabla en particular, tenemos la opción de generar la información basandonos en un campo en particular, por defecto, esta ip_address, para cambiarlo hay que usar el comando SET. Tambien podemos decidir si queremos Nulls en nuestro reporte o valores repetidos o unicos. 

{% highlight sql linenos %}

[recon-ng][default] > use reporting/list
[recon-ng][default] > show info

{% endhighlight %}

## Formato XLSX

Con el modulo _reporting/xlsx_ exportamos nuestra base de datos entera en un fichero excel, usando una pagina por cada tabla. En este metodo no hay otras opciones ni variables que actualizar. 

{% highlight sql linenos %}

[recon-ng][default] > use reporting/xlsx
[recon-ng][default] > show info

{% endhighlight %}

## Formato XML

Ya el ultimo formato al que podemos exportar nuestros datos es el formato XML, para ello usaremos el modulo _reporting/xml_ en este modulo podemos seleccionar las tablas que queremos exportar mediante el comando SET TABLES, separando cada una por comas.

{% highlight sql linenos %}

[recon-ng][default] > use reporting/xml
[recon-ng][default] > show info

{% endhighlight %}

