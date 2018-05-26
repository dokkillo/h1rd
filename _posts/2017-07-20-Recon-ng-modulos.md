---
layout: post
title: Trabajando con los modulos de Recon-ng
category: Hacking
comments: true
description: Lo mejor de Recon-ng son sus modulos, en el post anterior hable de algun modulo por encima, mi idea en este articulo es centrarme en los modulos y sus funcionalidades.

tags:   

    - pentesting
    - recon-ng

---

Lo mejor de Recon-ng son sus modulos, en el post anterior hable de algun modulo por encima, mi idea en este articulo es centrarme en los modulos y sus funcionalidades.

## Como ejecutar un modulo en Recon-ng

Para ejecutar un modulo en recon-ng hay que ejecutar los siguientes comandos:

{% highlight sql linenos %}

[recon-ng][default] > show modules
[recon-ng][default] > use nombre_del_modulo
[recon-ng][default] > show info
[recon-ng][default] > run

{% endhighlight %}

* show modules para ver la lista de todos los modulos disponibles
* use nombre_del_modulo con esto entraremos dentro del modulo
* show info, para ver informacion del modulo y que necesitamos para ejecutarlo
* run, ejecutamos el modulo.


## Modulos de Recon-ng en profundidad


Antes de ejecutar cualquier modulo en Recon-ng, lo principal es ejecutar la opción show info, para ver que es lo que hace el modulo, y ver necesitamos para ejecutar el modulo, por ejemplo en la imagen, podemos ver un show info del modulo whois_pocs.

<figure>
<img alt="modulos de recon-ng" src="/resources/images/recon-ng.png"/>
<figcaption>
Información del modulo whois_pocs de recon-ng 
</figcaption>
</figure>

Como podeis ver, la informacion del modulo esta compuesta en varias secciones, son las mismas en todos los modulos. Las secciones son las siguientes:

* Description, descripción de lo que hace el modulo.

* Options, opciones de lo que necesita el modulo para trabajar correctamente, estas opciones se pueden rellenar mediante el comando set.

{% highlight sql linenos %}

[recon-ng][default] > set source elmundo.com

{% endhighlight %}

* Source options, aqui podemos ver sobre que tabla cogera los registros, puede que esa tabla este vacia, ya que no la añamos rellenado antes, y de un error al ejecutar el modulo, o que queramos hacer una query en especial.

{% highlight sql linenos %}

[recon-ng][default] > run select * from domains

{% endhighlight %}

## Listado de modulos de Recon-ng
keys add nombre_key_api key
Cuando ejecutamos show modules, la aplicación nos devuelve la lista que hay debajo, como puedes ver hay 5 categorias,

* Discovery
* Explotation, modulos de explotación
* Import, importacion de datos de fuentes externas
* Recon, todos los modulos de reconocimiento
* Reporting , para extraer los datos que hemos extraido de los modulos anteriores


{% highlight sql linenos %}

Discovery
  ---------
    discovery/info_disclosure/cache_snoop
    discovery/info_disclosure/interesting_files
keys add nombre_key_api key
  Exploitation
  ------------
    exploitation/injection/command_injector
    exploitation/injection/xpath_bruter

  Import
  ------
    import/csv_file
    import/list

  Recon
  -----
    recon/companies-contacts/bing_linkedin_cache
    recon/companies-contacts/jigsaw/point_usage
    recon/companies-contacts/jigsaw/purchase_contact
    recon/companies-contacts/jigsaw/search_contacts
    recon/companies-contacts/linkedin_auth
    recon/companies-multi/github_miner
    recon/companies-multi/whois_miner
    recon/contacts-contacts/mailtester
    recon/contacts-contacts/mangle
    recon/contacts-contacts/unmangle
    recon/contacts-credentials/hibp_breach
    recon/contacts-credentials/hibp_paste
    recon/contacts-domains/migrate_contacts
    recon/contacts-profiles/fullcontact
    recon/credentials-credentials/adobe
    recon/credentials-credentials/bozocrack
    recon/credentials-credentials/hashes_org
    recon/domains-contacts/metacrawler
    recon/domains-contacts/pgp_search
    recon/domains-contacts/whois_pocs
    recon/domains-credentials/pwnedlist/account_creds
    recon/domains-credentials/pwnedlist/api_usage
    recon/domains-credentials/pwnedlist/domain_creds
    recon/domains-credentials/pwnedlist/domain_ispwned
    recon/domains-credentials/pwnedlist/leak_lookup
    recon/domains-credentials/pwnedlist/leaks_dump
    recon/domains-domains/brute_suffix
    recon/domains-hosts/bing_domain_api
    recon/domains-hosts/bing_domain_web
    recon/domains-hosts/brute_hosts
    recon/domains-hosts/builtwith
    recon/domains-hosts/certificate_transparency
    recon/domains-hosts/google_site_api
    recon/domains-hosts/google_site_web
    recon/domains-hosts/hackertarget
    recon/domains-hosts/mx_spf_ip
    recon/domains-hosts/netcraft
    recon/domains-hosts/shodan_hostname
    recon/domains-hosts/ssl_san
    recon/domains-hosts/threatcrowd
    recon/domains-vulnerabilities/ghdb
    recon/domains-vulnerabilities/punkspider
    recon/domains-vulnerabilities/xssed
    recon/domains-vulnerabilities/xssposed
    recon/hosts-domains/migrate_hosts
    recon/hosts-hosts/bing_ip
    recon/hosts-hosts/freegeoip
    recon/hosts-hosts/ipinfodb
    recon/hosts-hosts/resolve
    recon/hosts-hosts/reverse_resolve
    recon/hosts-hosts/ssltools
    recon/hosts-locations/migrate_hosts
    recon/hosts-ports/shodan_ip
    recon/locations-locations/geocode
    recon/locations-locations/reverse_geocode
    recon/locations-pushpins/flickr
    recon/locations-pushpins/instagram
    recon/locations-pushpins/picasa
    recon/locations-pushpins/shodan
    recon/locations-pushpins/twitter
    recon/locations-pushpins/youtube
    recon/netblocks-companies/whois_orgs
    recon/netblocks-hosts/reverse_resolve
    recon/netblocks-hosts/shodan_net
    recon/netblocks-ports/census_2012
    recon/netblocks-ports/censysio
    recon/ports-hosts/migrate_ports
    recon/profiles-contacts/dev_diver
    recon/profiles-contacts/github_users
    recon/profiles-profiles/namechk
    recon/profiles-profiles/profiler
    recon/profiles-profiles/twitter_mentioned
    recon/profiles-profiles/twitter_mentions
    recon/profiles-repositories/github_repos
    recon/repositories-profiles/github_commits
    recon/repositories-vulnerabilities/gists_search
    recon/repositories-vulnerabilities/github_dorks

  Reporting
  ---------
    reporting/csv
    reporting/html
    reporting/json
    reporting/list
    reporting/proxifier
    reporting/pushpin
    reporting/xlsx
    reporting/xml

{% endhighlight %}

Como te has podido fijar, la sección más grande, es la sección de Recon, esta internamente esta organizada por grupos (contactos, compañias, host, dominios) que esta relacionado con la tabla donde se van a añadir los datos.

## API Keys

Como has podido ver, hay modulos, de facebook, linkedin, twitter, github, que requieren que añadamos una key de esa api para asi autentificarnos y poder usar el modulo.

Para hacerlo:

{% highlight sql linenos %}

[recon-ng][default] > show keys
[recon-ng][default] > keys add nombre_key_api key

{% endhighlight %}

* show keys nos muestra todas las keys que tenemos disponibles para usar asi como el nombre de la key
* keys add este comando nos ayudara a añadir la key




