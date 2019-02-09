---
layout: post
section-type: post
title: Métricas y feedback
category: WebsiteProject
tags: [ 'Jacob Uribe Ais', 'jacob', 'Tech', 'Webpage', 'getting-started', 'Analytics', 'Web', 'Disqus', 'Cookieconsent' ]
---

# Métricas y feedback

## Introducción
Ahora mismo tenemos una web funcional, en http, en nuestro servidor.
No obstante, me gustaría saber cuanta gente accede a esta web y información general del público del site: opiniones, horas de mayor acceso, etc.

El hecho de tener feedback e información, será el que nos permitirá después poder seguir avanzando y decidir qué posts tienen mayor impacto y aportan valor a nuestra página web.

Para ello, en esta primera fase de diseño de adquisición de datos, incorporaremos dos utilidades:

* Google Analytics: Nos dará métricas del uso de nuestra web.
* Disqus: Nos permitirá añadir un campo para cada post, mediante el cual nuestro público objetivo podrá poner comentarios a nuestras publicaciones.
* Cookieconsent: Informará al usuario de que este website utiliza cookies.


## Pasos previos: GDPR

Para intentar cumplir la GDPR, primero de todo, debemos informar al usuario de que en nuestra web vamos a usar cookies, en este caso, cookies de terceros. Añadiremos una nota conforme esta web hace uso de cookies mediante el proyecto [cookieconsent]([Cookieconsent](https://github.com/insites/cookieconsent/)).


En la web de [Cookieconsent](https://cookieconsent.insites.com/download/) se ofrece un editor visual para poder personalizar nuestra ventana emergente.

Tras jugar un poco con este editor, el resultado es:

```html

<link rel="stylesheet" type="text/css" href="//cdnjs.cloudflare.com/ajax/libs/cookieconsent2/3.1.0/cookieconsent.min.css" />
<script src="//cdnjs.cloudflare.com/ajax/libs/cookieconsent2/3.1.0/cookieconsent.min.js"></script>
<script>
window.addEventListener("load", function(){
window.cookieconsent.initialise({
  "palette": {
    "popup": {
      "background": "#00ff00",
      "text": "#ffffff"
    },
    "button": {
      "background": "#009900",
      "text": "#ffffff"
    }
  },
  "position": "bottom-right"
})});
</script>

```

Os recomiendo que, en función del proyecto para el cual estéis haciendo la web, invirtáis por lo menos una hora en escribir una página de cookies. Si es para una empresa, esto es obligatorio.

El código resultante lo añadiremos en el footer de todas nuestras páginas. En mi caso lo he añadido en: **_includes/js.html**.


## Analytics

Para obtener un código de analytics, accederemos a su [página](http://analytics.google.com) y nos registraremos. Si creamos una cuenta nueva, nos hará un test, donde es especificaremos todos los datos requeridos. Una vez acabado el test, apretaremos al botón "Obtener id de seguimiento" y nos leeremos y aceptaremos las condiciones

Una vez hecho esto, obtendremos ya un id de seguimiento. Hay que ponerlo en el archivo de configuración de Jekyll:

```yml
google-tracking-id: "UA-XXXXXXXXXX-X"
```
Si usas otro template, es posible que tenga otro nombre, o bien que Google Analytics no esté integrado.

Para los más aventureros, por si a alguien no le convence esto o quiere alguna alternativa a Google Analytics, hay otras opciones.
Hace ya mucho tiempo, usé Piwik, y funcionaba muy bien. El funcionamiento es muy similar a GOogle Analytics. Quizás en un futuro me plantee hacer evolucionar esto hacia una solución basada en Piwik, no obstante, por ahora y con el tráfico que espero que esto tenga (muy pocos accesos al día) es suficiente Google Analytics.


Un buen motivo para pasar a Piwik es el exceso de peticiones a Google Analytics, ya que si usamos una cuenta gratuita, tenemos algunas "limitaciones". Eso sí, recaerá sobre nosotros la responsabilidad de que todo funcione bien.


## Disqus

**Disqus** es una plataforma para conectar con tu audiencia. Te permite añadir un campo de comentarios en tus publicaciones y así poder tener feedback de tu público objetivo.

Personalmente me gustaría desarrollar esta funcionalidad, pero eso formará parte de trabajo futuro, ya que quiero probar esta plataforma desconocida para mí hasta ahora.

Para integrarla en este template de Jekyll, simplemente he tenido que registrarme en la web de [Disqus](https://disqus.com), crear un canal para mi web y añadir el identificador de Disqus en la variable **disqus-shortname** de nuestro archivo de configuración.

```yml
disqus-shortname: "..."
```



Una vez con todo esto aplicado, deberíais observar ya un campo para poner comentarios, así como deberíais empezar a recibir en breves datos de Analytics.

![Captura de pantalla del campo de comentarios](/img/screenshots/p4_1.jpg){:class="img-responsive"}


Esto va pillando color :)


Jacob Uribe Ais :)
