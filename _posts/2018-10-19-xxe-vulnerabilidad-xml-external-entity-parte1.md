---
layout: post
title:  XML, DTDs y Entidades (XXE 1)
category: Hacking
comments: true
description: La vulnerabilidad de XML External Entity o XXE (como se la conoce) se basa en un sistema deficiente al parsear los XMLs que recibe la aplicación web, permitiendo la inyección de entidades externas de XML posibilitando ataques como conseguir ficheros del servidor de producción o ejecucción de codigo. En el fondo, sucede igual que en el SQL inyection (SQLi) nunca te fies de lo que recibes del usuario.
tags:   

    - owasp
    

---

La vulnerabilidad de XML External Entity o XXE (como se la conoce) se basa en un sistema deficiente al parsear los XMLs que recibe la aplicación web, permitiendo la inyección de entidades externas de XML posibilitando ataques como conseguir ficheros del servidor de producción o ejecucción de codigo. En el fondo, sucede igual que en el SQL inyection (SQLi) nunca te fies de lo que recibes del usuario.

<figure>
<img alt="Ejemplo de un ataque usando la vulnerabilidad Xml External Entity (XXE)" class="img img-responsive" src="/resources/images/xxe_ejemplo_xml_external_entitity.jpg"/>
<figcaption>
Ejemplo de un ataque usando la vulnerabilidad Xml External Entity (XXE)
</figcaption>
</figure>

## XML

Para poder enteder que es un XXE, lo primero que necesitamos entender que es es un XML y lo que se considera una entidad. XML significa Extensible Markup Language, es decir es un lenguaje de Marcado Extensible, parecido al HTML pero en vez de mostrar los datos, el XML los describe. Su función principal es ayudar a pasar información entre varias aplicaciones, ya que una aplicación sabe que y como tiene que enviar la información y la aplicación que espera, sabe que tiene que recibir.

Esto es un ejemplo de un XML

{% highlight xml linenos %}

<?xml version="1.0" encoding="UTF-8" ?>
<Edit_Mensaje>
     <Mensaje>
          <Remitente>
               <Nombre>Nombre del remitente</Nombre>
               <Mail> Correo del remitente </Mail>
          </Remitente>
          <Destinatario>
               <Nombre>Nombre del destinatario</Nombre>
               <Mail>Correo del destinatario</Mail>
          </Destinatario>
          <Texto>
               <Asunto>
                    Este es mi documento con una estructura muy sencilla 
                    no contiene atributos ni entidades...
               </Asunto>
               <Parrafo>
                    Este es mi documento con una estructura muy sencilla 
                    no contiene atributos ni entidades...
               </Parrafo>
          </Texto>
     </Mensaje>
</Edit_Mensaje>

{% endhighlight %}

El codigo de arriba es un ejemplo basico de un XML, donde se puede ver los datos estructurados, un tipo llamado edit_mensaje, que contiene un mensaje, y este a la vez esta separado en remitente, destinatario, y texto.

{% highlight xml linenos %}

<?xml version="1.0" encoding="UTF-8" ?>
<Show_Mensajes>
     <Mensaje>
          <Remitente>
               <Nombre>Nombre del remitente</Nombre>
               <Mail> Correo del remitente </Mail>
          </Remitente>
          <Destinatario>
               <Nombre>Nombre del destinatario</Nombre>
               <Mail>Correo del destinatario</Mail>
          </Destinatario>
          <Texto>
               <Asunto>
                    Este es mi documento con una estructura muy sencilla 
                    no contiene atributos ni entidades...
               </Asunto>
               <Parrafo>
                    Este es mi documento con una estructura muy sencilla 
                    no contiene atributos ni entidades...
               </Parrafo>
          </Texto>
     </Mensaje>
     <Mensaje>
          <Remitente>
               <Nombre>Nombre del remitente</Nombre>
               <Mail> Correo del remitente </Mail>
          </Remitente>
          <Destinatario>
               <Nombre>Nombre del destinatario</Nombre>
               <Mail>Correo del destinatario</Mail>
          </Destinatario>
          <Texto>
               <Asunto>
                    Este es mi documento con una estructura muy sencilla 
                    no contiene atributos ni entidades...
               </Asunto>
               <Parrafo>
                    Este es mi documento con una estructura muy sencilla 
                    no contiene atributos ni entidades...
               </Parrafo>
          </Texto>
     </Mensaje>

</Show_Mensajes>

{% endhighlight %}

En este caso, es parecido al anterior pero es un xml que acepta listas.

## DTD


El DTD significa la Definición Tipo Documento, es el fichero que se ocupa de decirle al parser del XML (motor del XML) como esta formado el XML.

Por ejemplo, este seria el xml anterior con un DTD.

{% highlight xml linenos %}

<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE Edit_Mensaje SYSTEM "Edit_Mensaje.dtd">
<Edit_Mensaje>
     <Mensaje>
          <Remitente>
               <Nombre>Nombre del remitente</Nombre>
               <Mail> Correo del remitente </Mail>
          </Remitente>
          <Destinatario>
               <Nombre>Nombre del destinatario</Nombre>
               <Mail>Correo del destinatario</Mail>
          </Destinatario>
          <Texto>
               <Asunto>
                    Este es mi documento con una estructura muy sencilla 
                    no contiene atributos ni entidades...
               </Asunto>
               <Parrafo>
                    Este es mi documento con una estructura muy sencilla 
                    no contiene atributos ni entidades...
               </Parrafo>
          </Texto>
     </Mensaje>
</Edit_Mensaje>

{% endhighlight %}

Y el DTD seria este:

{% highlight xml linenos %}

<?xml version="1.0" encoding="ISO-8859-1" ?>
<!-- Este es el DTD de Edit_Mensaje -->

<!ELEMENT Mensaje (Remitente, Destinatario, Texto)*>
<!ELEMENT Remitente (Nombre, Mail)>
<!ELEMENT Nombre (#PCDATA)>
<!ELEMENT Mail (#PCDATA)>
<!ELEMENT Destinatario (Nombre, Mail)>
<!ELEMENT Nombre (#PCDATA)>
<!ELEMENT Mail (#PCDATA)>
<!ELEMENT Texto (Asunto, Parrafo)>
<!ELEMENT Asunto (#PCDATA)>
<!ELEMENT Parrafo (#PCDATA)>

{% endhighlight %}

En el caso del ejemplo, el DTD viene referenciado a un fichero externo, no tiene porque podria venir integrado en el propio XML.

## Las entidades del DTD

Las entidades del DTD, son un mecanismo simple de remplazo, por ejemplo si usaramos en el xml algunos caracteres, este podria hacer que fuese no valido, hay dos tipos de entidades, los parametros de entidades, y las entidades generales.

### Entidades generales

Estas entidades se declaran en el DTD pero la sustitución la realiza el parser, según lo marcado por el DTD. En el ejemplo siguiente se puede ver un ejemplo de una entidad general.

{% highlight xml linenos %}

    <!ENTITY gt       "&#62;"> 

{% endhighlight %}

La estructura de una entidad general es la siguiente:

{% highlight xml linenos %}

    <!ENTITY nombre_de_la_entidad "literal">

{% endhighlight %}

En este caso, nombre_de_la_entidad seria el nombre de la variable por la que sustituiremos, y literal el valor por el cual sustituiremos.

Tambien podemos extraer el valor del literal de un fichero que nosotros digamos, con SYSTEM

{% highlight xml linenos %}

    <!ENTITY nombre_de_la_entidad SYSTEM "ruta_de_sistema">

{% endhighlight %}


O podemos extraer ese valor de una URL externa, con PUBLIC, un ejemplo de ello seria:

{% highlight xml linenos %}

    <!ENTITY nombre_de_la_entidad PUBLIC  "identificador_publico" "url_de_un_documento">

{% endhighlight %}

### Los parametros de entidad

Los parámetros de entidad es una manera de crear variables internas del DTD que ayudan a que no se repita codigo.

En el ejemplo, %Inline seria un parametro de entidad.

{% highlight xml linenos %}

 <!ENTITY % Inline "(#PCDATA | a | br | span | bdo | map | object | 
                        img | tt | i | b | big | small | em | strong | dfn | 
                        code | q | samp | kbd | var | cite | abbr | acronym | 
                        sub | sup | input | select | textarea | label | 
                        button | ins | del | script)*">        
            
    <!ELEMENT p %Inline;>
    
    <!ELEMENT h1 %Inline;>
    
    <!ELEMENT h2 %Inline;>

{% endhighlight %}


## La vulnerabilidad del XXE

Si has prestado atención, seguramente te hayas preguntado, que pasaria si en la entidad System, le paso la ruta de otro fichero, o en Public le paso otra url, pues alli empieza el XXE. 

En el proximo articulo de este post, entrare en profundidad con la vulnerabilidad de XML External Entities.

Hasta la proxima