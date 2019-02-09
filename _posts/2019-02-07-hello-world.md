---
layout: post
section-type: post
title: Hello World
category: WebsiteProject
tags: [ 'Jacob Uribe Ais', 'jacob', 'Personal', 'Tech', 'Webpage', 'getting-started', 'Jekyll', 'Web' ]
---


# Hola mundo

## Introducción
Estos días que tengo libre, voy a dedicarme a hacer lo que siempre digo que quiero hacer pero para lo cual no suelo tener tiempo.

De hecho, pienso que estoy más ocupado ahora que antes, pero es más divertido. :smile:

Esta página web es uno de esos proyectos.


## Idea inicial
Primero me planteé: Qué puedo hacer para darme visibilidad y enseñar cómo trabajo?
Por este motivo me plantee aprovechar los dos dominios web que ya hace mil años que tengo contratados a la espera de una página web, y usarlos aprovechando mis conocimientos para que me cueste lo más mínimo hacer una página web, tanto a nivel de costes económicos, como a nivel de costes de tiempo.

Me gusta pensar a lo grande pero planificar todo en pasos pequeños. A alguien le suena Agile y/o Scrum? Pues planteo lo siguiente: tener algo nuevo al final de cada pequeña ejecución.
Así pues, volviendo a pensar en grande, mi objetivo a nivel tecnológico es tener una página web que me de un coste ínfimo ~1€/mes, capaz de aceptar millones de peticiones concurrentes. No es necesario que mencione que ha de ser resistente a ataques DDoS y tener en cuenta diferentes aspectos en seguridad como lo es el uso de SSL. Me gustaría poder monitorizar cuanta gente accede a mi website, así como posicionarlo mediante SEO (De este último campo me tendré que documentar bastante aún).
Aparte, ha de ser fácilmente modificable: Tengo que poder actualizarlo regularmente y con cierta facilidad, como si fuera un blog (teniendo en cuenta que soy un FullStack/DevOps, quizás esto deje fuera, hasta que no me lo replantee, a gente de fuera de mi sector o a gente de rango tecnológico más próxima a un "nivel usuario"), aunque intentaré explicarme con un nivel apto para todos los públicos. Esta web va a ser estrictamente para uso lúdico y personal: A día de hoy no me he planteado en ningún momento vender nada a través de ella. Es posible que si intentas usar el código que haré y los pasos que seguiré, deberás añadir nuevos puntos y tener en cuenta más cosas que, por el momento, yo no contemplaré.

Así pues, como de momento no tengo ni tan siquiera una página web, planteo una primera solución: Usaré un servidor centralizado típico (un VPS de una empresa aleatoria que no mencionaré), con un Apache/Nginx típico sin modificar, etc. Hago esta selección, porqué el VPS ya lo tengo contratado de hace tiempo. No obstante, mi solución debería ser compatible con un hosting de los más baratos, para reducir costes (Ideas random de hacia donde evolucionará todo: AWS S3, GitHub Pages,...).

Esto me plantea la opción de hacer una web directamente en HTML+CSS+Javascript. Evitando usar lenguajes de ejecución en servidor.
Esta opción es válida según el punto de vista de la economía: podremos tener una web funcional en un servicio hosting muy barato.
No obstante... Esta solución es fatal a nivel de desarrollo: Tendré que crear todo el html, css, javascript,... de las nuevas páginas!!! Ufff... los ingenieros somos vagos por naturaleza xD (Ya veréis que esto lo repito muy habitualmente).


## Jekyll: Un generador de webs estáticas

Y, es aquí cuando recurro a una herramienta de la cual mi amigo [Esteban](https://nanusefue.io/) ([nanusefue](https://github.com/nanusefue) en GitHub) me habla siempre, llamada Jekyll: Un generador de html mediante archivos de texto llano. La transformación del texto a una web con cara y ojos la llevaremos a cabo en nuestro ordenador, y subiremos a nuestro servicio de hosting, o vps, o servidor dedicado, ... Exclusivamente la web (html+css+javascript) ya generada.

Así como punto de partida, no voy a centrarme en el diseño de la web. Tengo amigos muy buenos en este campo que, de seguro que me podrán echar un cable llegado el momento. De momento voy a utilizar algún template ya generado de Jekyll por un tercero. No es necesario buscar mucho, simplemente en google puedes buscar: "Jekyll templates" y escoger el que más te guste. Es importante revisar antes las licencias para asegurarte de que el uso que le vas a dar a ese código sea acorde a la licencia que este tiene atribuida. Ten en cuenta que quizás tengas que pagar para hacer algún uso comercial, etc. Es muy importante tener esto en cuenta.

Por mi parte, he escogido un template básico para empezar. Su autor, Panos Sakkos, se hace llamar le4ker en GitHub y aprovecho para saludarle y darle las gracias por su trabajo. Podéis ver el proyecto original en [su repositorio](https://github.com/le4ker/personal-jekyll-theme) .

Para empezar a trabajar, he hecho un fork de este proyecto, ya que no descarto modificar aspectos en un futuro no muy lejano. El fork que comento, lo podéis encontrar en [GitHub](https://github.com/jeicob22/personal-jekyll-theme).

Los cambios han llegado antes de lo que esperaba. Veréis que he tenido que modificar algunas dependencias, entre ellas, algunas librerías las he cambiado de sección, como jemoji y jekyll-paginate, las cuales he movido de la sección plugins a gems para que todo funcione correctamente con las últimas versiones (a día de hoy).


Aparte, el proyecto original de Panos Sakkos me ha gustado porqué ya tiene un archivo de docker-compose para levantar todo, en el caso de que no quieras descargar nuevas dependencias y liarte a instalar Ruby, jekyll, etc. Hoy no explicaré ni usaré docker ni docker-compose. Lo reservamos para otro día.

De momento, parto de la idea de que todo el mundo tiene o quiere tener ruby y ruby gems instalado en su OS. Actualmente uso un Ubuntu 18.04. Para instalar todo esto, he ejecutado:

```bash
sudo apt-get install ruby-full build-essential zlib1g-dev
sudo gem install jekyll bundler
```

Aparte, para el template que uso, he tenido que instalar también:

```bash
sudo apt-get install ruby-dev zlib1g-dev
sudo gem install jemoji
sudo bash ./scripts/install
```

Ten en cuenta que igual el template que uses puede necesitar más (o menos) cosas.


Una vez hecho esto, podemos levantar nuestra web en local. Para ello, el template que uso ya tiene comandos creados en la carpeta de scripts:


```bash

./scripts/serve

```

Si usas otro template, simplemente puedes ejecutar un comando similar a:

```bash
cd CARPETA/DEL/PROYECTO
jekyll serve --watch --host "127.0.0.1" --config _config.yml,_config.dev.yml

```

Esto debería levantar una web en tu ordenador en el puerto 4000.


## Configuración vs código

Llegado aquí, quiero resaltar la importancia de diferenciar entre lo que es configuración y lo que es código.
Todos los proyectos software suelen tener una arquitectura definida (MVC, MVVM,...) y creo que esto en la carrera de informática e, inclusive, a veces a los de telecomunicaciones, lo suelen destacar. No obstante, cuando salimos de la carrera, a algunos profesores de la universidad se les ha olvidado diferenciar entre lo que es código y lo que es configuración de una aplicación. La configuración debería, por lo general, estar fuera del proyecto software. Nosotros, en nuestro proyecto Jekyll, podemos añadir un archivo de configuración de ejemplo, como lo ha hecho Panos. Este archivo de configuración nos servirá de punto de partida para crear nuestro archivo de configuración propio y privado, así como a otra gente le será útil para entender cómo funciona nuestro aplicativo. En este archivo de configuración podremos poner todos los parámetros. Además, el tener diferentes archivos de configuración, nos permite reutilizar el código en otros proyectos y modificar su comportamiento simplemente modificando un único archivo, garantizando un código desacoblado y altamente reutilizable.


Si hemos observado el archivo *_config.yml*, este contiene parámetros que quizás sí que nos gustaría tener controlados en nuestro gestor de versiones (git). Pero hay otros parámetros que quizás no nos interese tenerlos ahí, como por ejemplo el parámetro: google-tracking-id .

Así pués, vamos a copiar el archivo de configuración propuesto por Panos:

```bash
mkdir -p custom_configs
cp _config.yml custom_configs/production_config.yml

```

Donde production_config.yml será la configuración que debemos tener oculta, referente al entorno de producción.

Dependiendo de si creéis o no que este archivo debe estar en el repositorio de código, lo añadiremos o no al archivo .gitignore . Yo considero una buena práctica **NO tener el archivo de configuración que puede contener información confidencial (passwords, etc) en un repositorio** y aún menos si es un repositorio público. Pero en este sector he visto de todo...

Yo NO quiero que este archivo esté en el repositorio de código. Para ello, añadiré la carpeta de configuraciones (custom_configs) al archivo .gitignore . Aparte, recuerda añadir en tus archivos de configuración la carpeta "custom_configs" en el campo "exclude", para evitar que accidentalmente, al generar el código de la web esta se suba.
Si estás considerando la opción de tener configuraciones en tu repositorio, revisa que sean solo las configuraciones que NO pongan tu sistema en compromiso de ninguna manera: Contraseñas, códigos únicos de identificación de usuario/empresa, etc. Por ejemplo, subir el código identificativo de google analytics de por sí puede parecer que no sea "crítico"... No obstante, ten en cuenta que si el repositorio se lo descargan 10.000 personas y esas 10.000 personas lo usan para su página web y, para rematar, tu o quién se encargue de ello, no tienes bien configurada tu cuenta de Google Analytics... vas a tener una buena fiesta para limpiar luego tus logs y entender bien los datos que Analytics te exponga.


Hemos de tener en cuenta que tendremos que gestionar los backups de la carpeta de configuraciones de alguna manera. De momento no entraremos aún en esto.


Así pues, modificaremos los datos que queramos de este archivo de configuración propia y ejecutaremos la nueva configuración.
Para ello he creado un nuevo script sh (Ya veremos maneras más elegantes de hacer todo esto) para ejecutar con esta configuración.
El nuevo script quiero que cargue por defecto las configuraciones base del archivo *_config.yml* y sobre-escriba las configuraciones necesarias definidas en el archivo de configuración del entorno. En este caso, las configuraciones especificadas en custom_configs/production_config.yml .

Si accedes al repositorio, el script que menciono ya existe. Si quieres creártelo tu mismo, simplemente ejecutando en la carpeta del proyecto algo similar a:

```bash
echo '#!/bin/bash
mkdir -p custom_configs

jekyll serve --watch --host "127.0.0.1" --config _config.yml,custom_configs/production_config.yml
' > scripts/serve-custom-local

sudo chmod 775 scripts/serve-custom-local
```

Customiza todo como creas conveniente. Yo he cambiado los textos del inicio, eliminado el link de pagos de Bitcoins y de Keybase, etc.

Una vez customizado todo esto, ya podemos ejecutar:



Ahora ya podremos ejecutar:

```bash

./scripts/serve-custom-local

```


## Mi primer post
Nuestra web está ya en marcha! (en local jeje :smile: )


Le falta mucho por customizar etc. No obstante, lo primero que haremos para dar ya por finalizado este post, será crear el primer post y eliminar los posts que hay de ejemplo.

Para eliminar los posts de ejemplo, solo hay que eliminar los archivos de la carpeta *_posts*.  Yo, en este repositorio, he eliminado ya los posts que Panos Sakos habia publicado. No obstante, en esos posts hacia un pequeño tutorial para poder personalizar la web a nuestro gusto. Si tenéis tiempo, os recomiendo que le echéis un vistazo en el proyecto original de este tema de Jekyll.

De momento, vamos a crear un nuevo post. Para ello, podemos o bien crear el archivo en lenguaje Markdown, con la cabecera de Jekyll a mano o bien ejecutar el script de creación de posts que el autor nos ofrece. Esta vez voy a crearlo con el script de Panos. No obstante, si estáis utilizando sublime text, Atom o similar os puede resultar también fácil.


Eliminaremos los antiguos posts mediante:

```bash
rm _posts/*

```


Para que Jekyll nos cree un nuevo post, deberemos ejecutar:

```bash

./scripts/newpost "hello_world"


```
Donde "hello_world" se puede modificar, siendo este el identificador que se usará en el path de la web para acceder al post (que no necesariamente el título del post), junto con la fecha de creación.

La ejecución del comando previo, nos dará un template similar a:

```text
---
layout: post
section-type: post
title: Title
category: Category
tags: [ 'tag1', 'tag2' ]
---
```


Añadir el título que se prefiera,la categoría, tags,...
En mi caso, este primer post tendrá esta cabecera:

```text
---
layout: post
section-type: post
title: Hello World! :)
category: Tech
tags: [ 'jacob', 'uribe', 'ais', 'personal', 'tech', 'webpage', 'getting-started' ]
---
```



Para ver los cambios, detendremos la web con ctrl+c y volveremos a encender el servidor para ver los cambios.

Y eh aquí el resultado:


![image-title-here](/img/screenshots/p1_1.jpg){:class="img-responsive"}


Hasta el próximo post! :smile:




Jacob Uribe Ais
