---
layout: post
section-type: post
title: Un poco de Estilo
category: WebsiteProject
tags: [ 'Jacob Uribe Ais', 'jacob', 'Tech', 'Webpage', 'Jekyll', 'Web', 'Markdown', 'Gimp', 'ImageMagick', 'Fonts', 'css' ]
---

# Un poco de estilo

Todo y que en el post anterior, ya he expuesto una primera solución para subir nuestro pequeño site, el enseñar los primeros resultados de mi web a terceras personas ([Carla](http://bluecarla.com)), me ha hecho darme cuenta del hecho de que soy "demasiado ingeniero" referente a la creación de websites. He dejado el diseño y estilos demasiado de lado.


Así pués, antes de subir mi página web a producción, le debo añadir un poco más de "color" y "customización", _"eliminando los lorem ipsum dolor..."_ y similares que el template original tenia.

Lector, ten algo en cuenta: Yo no soy diseñador. Habrán mil cosas que se podrán mejorar y estoy más que abierto a críticas (constructivas). No obstante, hay las típicas "cositas" que hasta un novato del diseño como yo si que sabe que debería cambiar y añadir:

* Estilo de los textos (Mediante Markdown language).
* Imágenes (Favicon, Logo,...).
* Eliminar las imágenes y textos de demo y adaptarlas a algo más de "mi gusto".
* ...

De momento, en este primer sprint de diseño y contenido de la página, no voy a añadir nuevas páginas ni secciones. Tenemos trabajo por delante!

## Markdown language

Por si alguien se lo estaba preguntando, el lenguaje que estoy usando en Jekyll es [Markdown language](https://es.wikipedia.org/wiki/Markdown). Si ya estás familiarizado/a con los README.md típicos de un proyecto Git, seguramente ya lo conozcas.

Para programar etc. suelo usar **Sublime Text 3**. No obstante, para editar Markdown language, prefiero usar el editor **Atom**, el cual ya tiene un intérprete de *Markdown Language* integrado mediante el cual podemos ir previsualizando los cambios que vamos realizando apretando la combinación de teclas **ctrl + shift + m**.

![image-title-here](/img/screenshots/p3_1.jpg){:class="img-responsive"}


## Logo + Favicon

No me voy a complicar mucho en esto: Me imagino un logotipo muy simple: Una "J", de mi nombre.
Para ello usaré Gimp y una fuente libre de derechos.

### Selección de fuente
Revisad que la fuente que vayáis a usar tenga los derechos adecuados para lo cual la vais a utilizar.
Hay mil páginas web, si es que no tenéis ya ninguna que os convenza. En Ubuntu hay que añadir las nuevas fuentes (por lo general con formato .ttf) en la carpeta .fonts dentro de tu carpeta de usuario: **"/home/$USER/.fonts/"**.

Por mi parte he escogido la fuente [**"Domestic Manners"**  de **"Cheapskate Fonts"**](https://dl.1001fonts.com/domestic-manners.zip).


### Edición (Gimp) + ImageMagick
No tiene mucho misterio. Abrimos Gimp (O Photoshop o lo que prefirais!!) y crearemos nuestro logo.
Es importante que, si ya tenias abierto Gimp cuando has incorporado la fuente, lo reinicies.

![image-title-here](/img/screenshots/p3_2.jpg){:class="img-responsive"}

He usado una imagen de 1024*1024 píxels. Pero ahora deberemos exportarla a otras resoluciones. De hecho, el autor de este template ya nos propone unas. En la carpeta img/web-app las vemos listadas:
* icon-144p.png
* icon-192p.png
* icon-36p.png
* icon-48p.png
* icon-72p.png
* icon-96p.png

Exportaremos nuestro logo a todas estas resoluciones... Soy al único al que le da pereza esto???  

...

-_"... Los ingenieros somos vagos por naturaleza..."_-

...

De nada ;) :

```bash
#/bin/bash

# Archivo resize_logo.sh
export FILE_EXT='.png'
export SRC_IMAGE_NAME='logo'$FILE_EXT
export OUT_PATH='out_logos/'
mkdir -p $OUT_PATH
function jacob_img_resize {
    src_img=$1
    img_size=$2
    out_path=$3
    extension=$4
    convert $src_img -resize $img_size $OUT_PATH'icon-'$img_size'p'$extension

}

jacob_img_resize $SRC_IMAGE_NAME 144 $OUT_PATH $FILE_EXT
jacob_img_resize $SRC_IMAGE_NAME 192 $OUT_PATH $FILE_EXT
jacob_img_resize $SRC_IMAGE_NAME 36 $OUT_PATH $FILE_EXT
jacob_img_resize $SRC_IMAGE_NAME 48 $OUT_PATH $FILE_EXT
jacob_img_resize $SRC_IMAGE_NAME 72 $OUT_PATH $FILE_EXT
jacob_img_resize $SRC_IMAGE_NAME 96 $OUT_PATH $FILE_EXT


```

Teniendo en la misma carpeta el script **resize_logo.sh** y **logo.png**, ejecutando:

```bash
bash resize_logo.sh
```

Deberia darte como resultado las imagenes redimensionadas dentro de **out_logos**.

Para obtener el Favicon, ejecutaremos:


```bash
convert logo.png -define icon:auto-resize=16 favicon.ico
```

Podeis añadirlo al archivo generado previamente.

Quiero que nos fijemos en algo más:

Ir a la url: http://localhost:4000/favicon.ico nos devuelve un error 404.

Los navegadores, por definición, antes de entrar en nuestra web, van a buscar el favicon ahí cuando hacen la predicción de la web que estás escribiendo en el campo de texto de tu navegador. De esta manera, nuestro favicon aparecerá en la barra superior del navegador cuando la gente esté escribiendo la url de nuestra web. Para conseguir esta funcionalidad, copiaremos el favicon.ico en la raíz de nuestro proyecto. De esta manera los navegadores, cargarán el favicon antes.


Como mi Favicon es blanco, no se verá bien en la barra del navegador cuando se busque mi web, tal como podemos observar:

![Favicon en el navegador](/img/screenshots/p3_3.jpg){:class="img-responsive"}

Para ello definiré dos Favicons, crearé uno con mi letra en negro, en la localización **/favicon.icon**
y otro con la letra en blanco, en el path carpeta **/img/blacktheme-favicon.ico** ya que el template usa un favicon claro sobre el fondo oscuro.


Aparte, modificaremos el campo **black-favicon** en **_config.yml**:

```yml
...

black-favicon: "/img/blacktheme-favicon.ico"

...
```

La foto de fondo de la página de inicio no me convence tampoco.
Por suerte hay diferentes webs que ofrecen imágenes de uso libre.

He encontrado esta foto de [David Clode](https://unsplash.com/photos/2slBHG3HtdA?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) en el banco de imágenes de [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText):

![Fotografia de una Rana por David Clode. Fuente: Unsplash](/img/intro-background-frog.jpg){:class="img-responsive"}

Las ranas siempre me han parecido muy _"cookies"_ :smile: jeje.

No obstante, la imagen me parece demasiado "chillona" y no deja leer bien el texto:
![Captura de pantalla del estado actual](/img/screenshots/p3_4.jpg){:class="img-responsive"}

Primero he declarado una nueva variable de color en el archivo **_sass/_variables.scss**:
```scss
...
// Custom color
$custom-color: #009900;
...

```

Mediante un poco de css, en el archivo css/grayscale.css, añadiendo esto dentro de las reglas para la clase _intro_:

```css
.intro {

 ...

&:before {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-image: linear-gradient(to bottom,$custom-color,#000000);
  opacity: .6;
}

...
/**/
}

```

Por ese motivo le he añadido una capa por encima con un gradiente mediante css, que va desde un verde hacia un negro:

![Captura de pantalla del resultado del gradiente](/img/screenshots/p3_5.jpg){:class="img-responsive"}




No sé si se habrá suicidado ya algún diseñador, pero desde mi ignorancia referente al diseño, creo que queda bien :smile:.

Para terminar de eliminar a los diseñadores que queden vivos, he decidido modificar la barra superior y hacer que cuando hacemos scroll hacia abajo se convierta en la misma tonalidad verde que hemos usado para el gradiente.

Dentro del archivo de **_sass/_variables.scss**,
Modificaremos el color del fondo de la barra superior:
```css
/**/
$navbar-lg-collapse-background-color: $custom-color;
/**/
```

Lo que se traduce en:

![Captura de pantalla del resultado del gradiente](/img/screenshots/p3_6.jpg){:class="img-responsive"}

Las aberraciones que se ven en la imagen, debajo de la barra superior verde, son aberraciones causadas por el proceso de compresión a jpg. En la web real estas no existen.


## Lorem ipsum dolor sit amet ...

Bueno, en esta sección me limitaré a modificar contenido ya existente que el autor original del template, Panos Sakkos, puso como ejemplo.

He revisado la página de inicio, etc. Si estás leyendo este post, entonces puedes ver el resultado navegando tu mism@ por la web.


## Fuentes
La fuente Lora, que viene por defecto en el template de la web, no me acaba de convencer. He decidido añadir la Roboto (que es la que se suele usar en Android y Material Design).
Se puede añadir desde Google Fonts, sin coste. Para ello, añadiremos la nueva fuente en el header de la web modificando el archivo **_includes/head.html**:

```html

<link href="https://fonts.googleapis.com/css?family=Roboto" rel="stylesheet">

```

Aparte, he tenido que modificar el css y añadirla.

Estoy pensando, que estaría guay que las cabeceras, en vez de usar Montserrat, usasen la fuente que he usado para el Logo, Domestic Manners. No obstante, solo dispongo de esta en formato .ttf, lo cual puede traducirse a diferentes incompatibilidades en algunos navegadores.

Googleando un poco, he encontrado una web que nos permitirá transformar la fuente a diferentes formatos, así como nos generará un html de ejemplo para saber cómo aplicar las fuentes llamada [Fontsquirrel](https://www.fontsquirrel.com/tools/webfont-generator).



La fuente convertida está en el directorio **fonts/**.

Solo es necesario añadir un poco más de css:

```css
@font-face {
    font-family: 'DomesticMannersRegular';
    src: url('/font/domestic_manners-webfont.woff2') format('woff2'),
         url('/font/domestic_manners-webfont.woff') format('woff'),
         url('/font/domestic_manners-webfont.ttf') format('truetype');

    font-weight: normal;
    font-style: normal;

}
```
También es necesario modificar el css que creamos necesario. Por ejemplo, dentro del archivo **css/grayscale.css**:

```css
.navbar-custom {
    margin-bottom: 0;
    border-bottom: 1px solid rgba($font-color, 0.3);
    text-transform: uppercase;
    font-family: "DomesticMannersRegular", "Montserrat","Helvetica Neue",Helvetica,Arial,sans-serif;
    ...
  }
  ...
  /**/
```


Añadiendo nuestra nueva fuente a la  barra de navegación. No obstante, tras hacer diversas pruebas, he decidido mantener La fuente Montserrat, ya que da una mayor sensación de "simplicidad".

Añadiré la fuente en un futuro en algún lado, pero aún estoy decidiendo donde. De momento la dejaré incluida en el proyecto y, en una segunda fase de estilos, le daré uso.


## Timeline

He modificado el timeline de muestra del autor original por uno más... adaptado a "mi estilo" :smile::

![Captura de pantalla del resultado del gradiente](/img/screenshots/p3_7.jpg){:class="img-responsive"}

## Contacto y email
La semana pasada vi a un tío hackear una cuenta de paypal usando solamente un hack del contestador automático del teléfono de la víctima.

No voy a meter mi email, aunque veo que el autor del template ya ha tenido en cuenta los bots que rastrean webs en busca de emails para spam. No he comprobado la eficacia de la protección que el autor ya ha añadido mediante Javascript. En vez de eso, he añadido en la lista de tareas por hacer, añadir un formulario de contacto.

## Idioma

De momento, para ir rápido, he desarrollado esta web solo en castellano. Y, para dar consistencia a esa decisión, he decidido traducir toda la web a castellano.

No obstante, en mi lista de funcionalidades a realizar (Yo prefiero llamarla lista de TODOs) he añadido: *"Multi-language"*.

Estoy pensando que puna nueva página de la web podría ser la lista de TODOs :smile: ¿Hay que apuntar esto a la lista de TODOs? (Entrando en un while en 3... 2... 1...).





Jacob Uribe Ais :)
