---
layout: post
title: Jugando con imágenes
category: 
tags: Jekyll, wiki
year: 2013
month: 12
day: 22
published: true
summary: Jugando con imágenes en Markdown con Jekyll
image:
---

En este post voy a hacer algunas pruebas con imágenes en un post. Para insertar una imagen
parece que basta con tener el fichero en una carpeta del sitio y hacer una referencia a 
dicha imagen.

No he visto ningún mecanismo para que Jekyll gestione las imágenes de una forma algo más
inteligente, como por ejemplo, el reescalado automático. 

Mi primera imagen en un blog va a ser el logo de Jekyll. 

![Jekyll](/img/posts/2013-12-22/jekyll.png)  

Para que se vea la imagen, he puesto el siguiente código en el post: 

    ![Jekyll](/img/posts/2013-12-22/jekyll.png)

Como se puede intuir, la parta más laboriosa de trabajar con imágenes está en que hay que darles
nombre y crear una carpeta por cada entrada para que no se mezclen.

Buscando por la red he visto [un plugin][] de Jekyll que hace el reescalado de las imágenes para
varias resoluciones. El problema es que si usamos plugins de Jekyll, no podremos aprovecharnos de
la generación automática del sitio por GitHub y tendremos que generar nosotros las páginas en 
local antes de subirlas. Si tenemos instalado Jekyll en local para previsualizar, esto no debería
ser un problema, pero el flujo no es tan automático. 

[un plugin]: https://github.com/robwierzbowski/jekyll-picture-tag