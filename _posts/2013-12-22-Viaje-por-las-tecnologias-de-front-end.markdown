---
layout: post
title: Viaje por las tecnologías de "front-end" (Parte 1)
category: 
tags: web, css, html, javascript
year: 2013
month: 12
day: 22
published: true
summary: Es este post os contaré cómo (y por qué) ha comenzado mi viaje por las tecnologías de "front-end".
image: viaje-front-end/html-css-js.jpg
---

Yo soy un desarrollador de software un poco atípico. Por mi trabajo como profesor, sólo puedo dedicar parte de mi 
tiempo de trabajo a programar. La otra parte la dedico a preparar material docente, corregir, leer libros de diversas tecnologías, etc. 
Además, en el último año también me he dedicado principalmente a la gestión de equipos y dirección técnica. Si me conoces,
sabes que me saqué el [certificado de Scrum Master][Scrum Master] hace un año.

[Scrum Master]: http://micaelgallego.blogspot.com.es/2013/05/soy-scrummaster-certificado-e-intento.html 

En el campo de la informática en general y del desarrollo software en particular, siempre hay que mantenerse al día. Yo siempre
intento mantenerme al día de mis tecnologías preferidas. Suelo estar bastante informado de las tecnologías relacionadas con Java
(Spring, Maven, Gradle, Java 8, Programación Concurrente en Java, Java EE, Android, ...). También me intereso por las buenas prácticas
(TDD, XP, Clean code, Agile, ...). Y debido al área de investigación al que me dedico, también suelo estar al día de diseño de algoritmos
de optimización.

Nunca he estado muy al día de las tecnologías web porque nunca he trabajado en ese área. Hace casi 10 años (en el 2004) impartí 
varios cursos de desarrollo web con Java: Servlets, JSP, HTML, JDBC. Hasta llegué a publicar un [artículo sobre el tema][HiMVC].
Por aquel entonces eso era la web. Pero obviamente las cosas han 
cambiado muchísimo desde aquellos días. Hace un par de años impartí la asignatura de Desarrollo de Aplicaciones Web en la [URJC][] y 
me reciclé bastante. Me puse al día con Java EE (EJB, JSF, JPA,...), pero la parte de front-end (HTML, CSS, JS, AJAX, ...) la impartió
otro profesor, así que no me puse mucho con esa parte.

[HiMVC]: http://www.foibg.com/ijita/vol13/ijita13-1-p10.pdf (Hi!MVC: Hierarchical MVC Framework for Web Applications)
[URJC]: http://www.urjc.es

Durante el año pasado estuve en contacto con la tecnología web. Aunque yo no programé la parte cliente, estaba de _scrum master_ 
y arquitecto de una aplicación web y móvil. La aplicación se llama [welvi][] y ofrece entrenamiento personal y servicios de actividad física. 
El caso es que estuvimos evaluando muchas tecnologías y muchas arquitecturas diferentes para implementar welvi. Decidimos implementar una API REST
consumida por las aplicaciones de cliente (Web JavaScript, Android, iOS y Samsung Smart TV). La tecnología de back-end la teníamos bastante 
clara. Se implementó con Spring y Tomcat. Estuvimos evaluando Mongo como sistema de persistencia y finalmente nos convenció.  

Pero el caso de front-end fue más complicado. Al principio estuvimos evaluando si hacer una web tradicional (en la que el servidor
genera HTML) o bien una web con cliente JavaScript ([Single Page Application][SPA]). Finalmente decidimos el enfoque de _Single Page Application_. 
Esa arquitectura nos permitía que la web fuera mucho más fluida e interactiva y además nos permitía implementar un único back-end con una API REST
para todos los clientes. 

[welvi]: http://www.welvi.es
[SPA]: http://en.wikipedia.org/wiki/Single-page_application

Y ahí empezó la explosión de tecnologías, técnicas, librerías, herramientas y frameworks para implementar la parte cliente, el front-end. Mi amigo
[Anthanh Pham][Anthanh] se encargó de bucear en este mar de caos y confusión para implementar el front-end de welvi. Después de varios meses de 
búsqueda, análisis, pruebas y prototipos, nos quedamos con las siguientes tecnologías, librerías, frameworks y herramientas:

 * **HTML**: Se usó únicamente contenido semántico para estructurar contenido.
 * **CSS**: Se utilizó [SASS][] como herramienta de generación de CSS con [COMPASS][].
 * **JavaScript** 
   * **Lenguaje** 
     * Sólo usamos [las partes buenas][GoodParts]. No nos hizo falta [CoffeScript][].
     * Intentamos no meter la pata usando [jslint][] y [jshint][].
     * Tenemos en cuenta los [patrones de diseño][] y el [patrón módulo][].
     * El código se "comprime" con [UglifyJS][].
     * Las dependencias en "runtime" se gestionan con [Requiere.js][]
   * **Librerías / Frameworks**
     * [jQuery][] para mejorar y unificar el acceso al DOM y otras funcionalidades del navegador.
     * [Underscore][] para gestionar las estructuras de datos y otras funciones de utilidades.
     * [Backbone][] Framework MVC con modelos y eventos ante cambios en el modelo.
     * [Marionette][] Librería de gestión de vista de Backbone.
   * **Gráficos**
     * [Bootstrap][] Como librería de componentes gráficos.
   * **Compatibilidad de navegadores**
     * Usamos [Modernizr][] para gestionar la compatibilidad con los navegadores con ([Pollyfills][])
 * **Herramientas**
   * [Yeoman][] para generar el esqueleto de la aplicación con las dependencias necesarias
   * [Grunt][] para ejecutar las tareas en el ciclo de vida del software (construcción, empaquetado, ejecución de test, etc...)
   * [Bower][] para gestionar las dependencias en "tiempo de construcción" (basado en [Node.js][] y [NPM][])

[Anthanh]: http://www.linkedin.com/pub/anthanh-pham-trinh/38/502/b05
[SASS]: http://sass-lang.com/
[COMPASS]: http://compass-style.org/
[GoodParts]: http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742
[CoffeScript]: http://coffeescript.org/
[jshint]: http://www.jshint.com/docs/
[jslint]: hhttp://jslint.com/
[UglifyJS]: https://github.com/mishoo/UglifyJS
[patrones de diseño]: http://addyosmani.com/resources/essentialjsdesignpatterns/book/
[patrón módulo]: http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html
[jQuery]: http://jquery.com/
[Underscore]: http://underscorejs.org/
[Bootstrap]: http://getbootstrap.com/
[Backbone]: http://backbonejs.org/
[Marionette]: http://marionettejs.com/
[Pollyfills]: https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills
[Modernizr]: http://modernizr.com/
[Yeoman]: http://yeoman.io/
[Bower]: http://bower.io/
[Grunt]: http://gruntjs.com/
[Node.js]: http://nodejs.org/
[NPM]: https://npmjs.org/
[Requiere.js]: http://requirejs.org/

También usamos tecnologías de testing, pero eso lo dejamos para otra entrada.

Mi objetivo es ponerme al día con todas estas tecnologías. Por mi propio interés (nunca hay que quedarse atrás) y para poder 
contar algo de esto en la asignatura que estoy a punto de empezar a la vuelta de Navidades. La web ha cambiado mucho desde la última vez que
estuve trabajando con ella, así que toca actualizarse.

Iré contanto mis peripecias en este viaje en más entradas sobre el **Viaje por las tecnologías de "front-end"** 

<div id="note">
{% capture myinclude %}{% include vtf.markdown %}{% endcapture %}
{{ myinclude | markdownify }}
</div>