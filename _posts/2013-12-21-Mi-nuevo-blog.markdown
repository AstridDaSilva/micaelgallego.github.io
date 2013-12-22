---
layout: post
title: Mi nuevo blog
category: Me
tags: me
year: 2013
month: 12
day: 21
published: true
summary: Presentación de mi nuevo blog
image: post_one.jpg
---

Hoy estreno nuevo blog. Aunque por fuera parezca un blog normal, por dentro es muy diferente a los 
blogs "tradicionales". 

Como puedes ver por la URL http://micaelgallego.github.io, el blog está alojado
en GitHub, la forja y red social para desarrolladores. La diferencia fundamental con otros tipos de 
blogs es que este blog es una página estática que se genera automáticamente partiendo de código wiki.
En concreto, el formato de wiki es Markdown y la herramienta de generación es [Jekyll][Jekyll].

El objetivo es tener una forma más sencilla y más directa de escribir entradas del blog que incluyan 
código fuente. Quizás cambie de opinión, pero creo que para mi es más sencillo escribir un nuevo post
en un fichero de texto en mi ordenador que conectado a una págin web de wordpress o blogger. Además, 
la sintaxis wiki es más amigable para escribir sobre código que escribir directamente en un editor wysiwyg
online. 

Al principio no entendía bien el workflow para crear el blog en github, pero después de echar un vistazo
a varias páginas ya me he enterado:

* Existe un generador de sitios web basado en formato wiki Markdown llamado [Jekyll][Jekyll].
* Este generado se puede usar en local y tiene un sistema de generación automática cuando el fichero cambia.
* Este sistema también está integrado en github, de forma que el contenido en formato wiki se transforma 
  automáticamente en HTML antes de ser publicado. Esto puede ser un poco confuso al principio, pero tiene
  la ventaja de que una vez creado el sitio, sólo tienes que preocuparte de subir ficheros en formato wiki 
  a git y la página se genera de forma automática.
  
La versión básica de Jekyll es un poco "minimalista", pero he encontrado 
[este blog](http://erjjones.github.io/blog/How-I-built-my-blog-in-one-day/) y me ha ayudado a poner a 
punto este sitio. Graficamente no es muy impactante, pero creo que cumple el objetivo, es fácil de editar.

Lo que ocurre es que ahora tengo que aprender un poco de Markdown. Yo soy más de Textile (el formato
de wiki que usa Redmine). He encontrado esta página con información sobre [Markdown](http://daringfireball.net/projects/markdown/syntax) que me está sirviendo como guía rápida.  
 
[Jekyll]: http://jekyllrb.com/

