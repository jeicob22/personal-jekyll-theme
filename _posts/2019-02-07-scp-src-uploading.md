---
layout: post
section-type: post
title: "Primera aproximación: scp"
category: WebsiteProject
tags: [ 'Jacob Uribe Ais', 'Jacob', 'Tech', 'Webpage', 'scp', 'getting-started', 'Apache' ]
---

# Subir la web mediante SCP

## Recapitulemos un poco

Hasta aquí hemos conseguido una web mínima funcional. Generamos los posts en texto llano y los transformamos a html mediante nuestro ordenador local. Esto nos da dos puntos positivos:

* No tenemos un programa que se ejecuta en nuestro servidor **(Hosting más barato)**
* No tenemos que programar directamente en HTML+CSS+Javascript si no que tenemos templates y una herramienta (Jekyll) que traduce el texto llano a código **(Bajo tiempo de desarrollo)**


## Introducción

Esto no es una herramienta Wordpress ni Drupal.
En un CRM como Wordpress y/o Drupal, tu te conectas a tu backoffice mediante tu /wp-admin o similar y administras sus funcionalidades desde tu navegador web. Creas nuevo contenido desde ahí, administras plugins y configuraciones, así como dispones de una base de datos que almacena los datos que se generan y un sistema de archivos que puedes "gestionar" también desde el backoffice, subiendo imágenes y contenidos.


Nuestra solución es diferente: tenemos una aplicación en nuestro ordenador de desarrollo que nos permite generar una web y una vez generada, deberemos subirla a nuestro espacio web. Nosotros no editamos la web desde un navegador. Esto no quiere decir que sea mejor ni peor, simplemente que tenemos unos requisitos que hemos marcado al principio: economía y facilidad en el desarrollo.

No obstante, a diferencia de un Wordpress, trabajar con Jekyll quiere decir que cada vez que queramos generar un nuevo post deberemos seguir los siguientes pasos (o similares):

1. Generar el nuevo archivo del post
2. Generar de nuevo los tags
3. Generar de nuevo las categorías
4. Generar de nuevo el código de la web
5. Testear que la web se ha generado bien
6. Subir el código generado

Así a simple vista, parecen demasiados pasos. Soy ingeniero, recordemos: vago por naturaleza.
No obstante, es solo el segundo post de esta web y que este es un proyecto que estamos empezando. De momento podemos permitirnos el lujo de tener 6 pasos para generar un nuevo post.
En un futuro citaremos de nuevo estos 6 pasos y miraremos cómo optimizarlos.



## Subiendo el código
Ahora ha llegado el momento de subir el código de nuestra web a un servidor/hosting.

Debido a que ya dispongo de un servidor VPS, voy a subir la web resultante ahí mediante SCP.

Si teneis un VPS o un servidor con SSH, podréis usar SCP. Si por el contrario habéis contratado un hosting más sencillo, seguramente podáis utilizar la herramienta Filezilla o un cliente ftp similar para subir vuestro código.


En ambos casos, tendremos que generar la página web final.

Vayamos por partes:

### 1. Generar un nuevo archivo de post

```bash
./scripts/newpost scp-src-uploading

```

Esto nos generará un nuevo archivo dentro de la carpeta **_posts**, al cual podremos agregar contenido, definir sus tags, etc.


## 2. Generar de nuevo los tags
```bash
./scripts/generate-tags

```

### 3. Generar de nuevo las categorias
```bash
./scripts/generate-categories

```
### 4. Generar de nuevo el código de la web
Para ello, haremos el build final mediante:

```bash
JEKYLL_ENV=production jekyll build --config _config.yml,_custom_configs/production_config.yml
```
### 5. Testear que la web se ha generado bien
De momento consideraremos que la web se ha generado bien si no ha habido ningún error de ejecución.
Os recomiendo que, en caso de duda, probéis que la web se abre correctamente y todo está en su sitio.
No obstante, esto no seria suficiente en un entorno real de producción. Futuramente recalcaremos este punto, ya que puede ser uno de los puntos clave que hagan de nuestra plataforma una plataforma robusta y sólida.

### 6. Subir el código generado
Para subir el código html generado, podemos usar scp. Más adelante ya nos liaremos con packer y/o Ansible.

Para subir mediante SCP, ejecutaremos:

```bash
scp -r _site user1@website.molona:/PATH/DE/DESTINO/.
```

Tenemos que tener en cuenta que /PATH/DE/DESTINO debería tener los permisos adecuados para que el usuario *user1* pueda escribir en él.



## Bonus track: Configurando Apache


Como ya he comentado, tengo un VPS de hace mil siglos contratado y por eso uso scp para subir el código. Herramienta que prefiero frente a ftp.


No obstante, para que podáis configurar bien Apache, en caso de que tengáis un Ubuntu 18.04, os expongo aquí como hacerlo.


Primero de todo, deberéis instalar apache:


```bash
sudo apt-get install apache2 -y
```

A partir de aquí, no necesitamos mucho más, dado que nuestro código ha sido transformado ya previamente en html+css+javascript en nuestra máquina de desarrollo. No hacemos uso de php ni otros lenguajes interpretados.


El archivo de configuración de apache podría ser, por ejemplo, el siguiente:


```text
<VirtualHost *:80>
	ServerName jacoburibeais.com

	ServerAdmin webmaster@localhost
	DocumentRoot /PATH/DE/DESTINO/_site

	# Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
	# error, crit, alert, emerg.
	# It is also possible to configure the loglevel for particular
	# modules, e.g.
	#LogLevel info ssl:warn

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

	# For most configuration files from conf-available/, which are
	# enabled or disabled at a global level, it is possible to
	# include a line for only one particular virtual host. For example the
	# following line enables the CGI configuration for this host only
	# after it has been globally disabled with "a2disconf".
	#Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet

<VirtualHost *:80>
    ServerName jacoburibeais.com
        ServerAlias jacoburibeais.com www.jacoburibeais.com
        ServerAdmin webmaster@jacoburibeais.com
        DocumentRoot /var/www/html/jacoburibeais.com

        <Directory /var/www/html/jacoburibeais.com>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/site-a_error.log
        CustomLog ${APACHE_LOG_DIR}/site-a_access.log combined
</VirtualHost>
```
Podriamos modificar el funcionamiento de Apache para que acepte más conexiones etc. pero de momento, lo dejaremos por hoy.


Jacob Uribe Ais
