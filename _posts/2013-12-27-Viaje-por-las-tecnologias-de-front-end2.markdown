---
layout: post
title: Primer contacto con JavaScript. Tecnologías Front-end (Parte 2)
category: front-end
tags: javascript
year: 2013
month: 12
day: 27
published: true
summary: Esta entrada es la segunda parte de mi "Viaje por las tecnologías de "front-end". En ella te cuento mi toma de contacto con JavaScript.
image: viaje-front-end/html-css-js.jpg
---

Esta entrada es la segunda parte de mi "Viaje por las tecnologías de "front-end". Si no lo has leído, te recomiendo que eches un vistazo al [primer post][Parte 1] en el que cuento cual es mi roadmap, qué tecnologías tengo pensado estudiar y por qué. 

Aunque he estado viendo algunas cosillas de HTML y CSS, todavía me queda darle un empujón a esa parte. Con lo que más he avanzado ha sido con JavaScript. Recomendado por [Anthanh][] me he leído el libro de [JavaScript: The good parts][GoodParts]. También he consultado algunas páginas oficiales de Mozilla y un par de preguntas en StackOverflow. A medida que vaya poniendo las notas de JavaScript pondré los links que he mirado.

[Juan Llado][jllado] me ha recomendado el libro [Secrets of the Javascript Ninja][JSNinja] del creador de jQuery. Todavía no le he echado un vistazo, pero seguro que es bastante completo.

[Parte 1]: http://micaelgallego.github.io/blog/Viaje-por-las-tecnologias-de-front-end/
[Anthanh]: http://www.linkedin.com/pub/anthanh-pham-trinh/38/502/b05 
[GoodParts]: http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742
[JSNinja]: http://www.manning.com/resig/
[jllado]: https://twitter.com/jllado

He decidido poner las conclusiones al principio, para que sepas lo que pienso de JavaScript después de mi primer contacto. 

Después viene un resumen de lo que he aprendido del lenguaje en los dos últimos días. He hecho el resumen asumiendo que el lector conoce Java (como en mi caso). De forma que sea rápido para un desarrollador de Java saber qué es igual y qué es diferente. 

Si controlas de JavaScript y ves alguna concepto mal explicado o erróneo. Ponme un comentario y me ayudarás a aprender. Si no tienes ni idea de JavaScript (como yo), a lo mejor te sirve de guía de aprendizaje ;)

# Conclusiones

## El libro "JavaScript: The Good Parts" 

* Es consiso y se centra en las buenas partes del lenguaje, pero bajo mi punto de vista está un poco desorganizado. Sobre todo para los que venimos de Java. Algunas cosas que me han parecido confusas o desorganizadas:
  * Cuenta los bloques try / catch junto con el resto de sentencias de control de flujo. Yo hablaría de excepciones en un tema aparte.
  * Describe aspectos propios de la reflexión cuando te está contando cómo son las funciones y los objetos. Supongo que en JavaScript es normal tratar los elementos de forma reflexiva por la naturaleza dinámica del lenguaje, pero los que venimos de un lenguaje con tipado estático normalmente usamos la reflexión "con cuidado".
  * La forma de explicar la orientación a objetos es un poco confusa, porque te explica varias formas de crear clases y objetos pero no concreta en cual es la mejor forma de hacerlo. Además, lo cuenta en diferentes partes del libro, cuando hubiera sido mejor agruparlo.
  * La explicación del patrón módulo me parece un poco confusa porque no lo relaciona con el concepto de clase al principio. 
  * Te describe idiomas de programación a la misma vez que te explica el lenguaje como "cascade" (fluent API) o memoization (variables de función que se inicializan la primera vez).

## Futuros pasos con el lenguaje

* Creo que finalmente he conseguido enterarme de los conceptos básicos del lenguaje. Aunque todavía me falta  mirarme más material antes de que pueda sentirme agusto con "el lenguaje" y los patrones básicos. En concreto:
  * [Patrones de diseño en JavaScript][PatronesJS]
  * [Patrón módulo][ModuloJS]
  * Librería [jQuery][]
  * Librería [Underscore.js][]


## ¿Qué pienso de JavaScript?

  * Todo lo que pensaba del lenguaje antes de aprender JavaScript lo sigo manteniendo: JavaScript es un mal lenguaje.
  * A mi no me gustan mucho los lenguajes con tipado dinámico, porque me gusta que el compilador me ayude lo más posible cuando me equivoco y me gustan las ayudas de los IDEs. Pero he usado otros lenguajes con tipado dinámico como Ruby y un poco Python y me parece que su modelo de orientación a objetos es muy razonable (muy similar a Java). No entiendo por qué JavaScript utilizó la programación orientada a objetos basada en prototipos.
  * Por lo que sé hasta ahora no hay consenso con la forma adecuada de representar los objetos. Mejor copiar todo en el objeto final? Mejor usar prototipos? Mejor usar ámbitos de funciones? La falta de un consenso y una forma aceptada de hacer bien las cosas creo que es negativa en un lenguaje.
  * El patrón módulo permite modularizar el programa y evitar colisiones en el objeto global, pero he encontrado poco soporte en las herramientas de depuración para este patrón. Por ejemplo, ¿Cómo puedo ver el contexto de una función sin estar parado en una sentencia suya en el depurador?
  * Cuando más aprendo JavaScript más me acuerdo de lo bueno que es tener una especificación formal del lenguaje en Java y un runtime certificado (la JVM). Buscar información sobre JavaScript en Internet es una odisea. No paro de econtrar frases como: "esto no se puede en este navegador (pero si en los demás)", "esto si se puede en la gran mayoría (pero no es estándar)", etc... Pasa lo mismo que en SQL.
  * El lenguaje tiene errores de diseño garrafales. Algunos son fáciles de solventar (no usando la funcionalidad maligna), pero otros están enraizados en el propio lenguaje.

## Las conclusiones de las conclusiones

* En definitiva, JavaScript es un mal lenguaje, pero no hay más remedio que usarlo porque es la plataforma más extendida del planeta. El creador del lenguaje tampoco tiene la culpa, supongo que nunca pensó que llegaría tan lejos.
* Supongo que cuando controle un poco de JavaScript tendré que mirar CoffeeScript o Dart, aunque no tengo claro si merece la pena otro nivel de indirección más ;).

[PatronesJS]: http://addyosmani.com/resources/essentialjsdesignpatterns/book/
[ModuloJS]: http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html
[jQuery]: http://jquery.com/
[Underscore.js]: http://underscorejs.org/

# Sintaxis básica

* La sintaxis básica está inspirada en Java y C.
* Tiene recolector de basura como Java.

## Mostrar información por pantalla

* document.write('Texto'): Escribe en el documento HTML.
* console.log('Texto'): Escribe en la consola JavaScript.

## Ejecución

* Documento .html que enlaza al código .js

{% highlight html %}
   <html>
     <head>
     	<link type="text/javascript" href="/js/script.js">
     </head>
     <body>
     </body>
   </html>
{% endhighlight %}   

* Fichero .js que contiene el código

## Comentarios

* Como en Java (una línea y multilínea)
* Se recomienda usar el de única porque no se puede comentar algunos tipos de expresiones regulares con el multilínea

## Palabras reservadas

* abstract
* boolean break byte
* case catch char class const continue
* debugger default delete do double
* else enum export extends
* false final finally float for function
* goto
* if implements import in instanceof int interface
* long
* native new null
* package private protected public
* return
* short static super switch synchronized
* this throw throws transient true try typeof
* var volatile void
* while with

## Delimitadores 

* Se usan {} y ; como en Java

## Tipos de datos

* Todos los valores son objetos. No existe la distinción entre tipos primitivos y objetos que hay en Java.
* Los tipos de datos básicos son: number, string, boolean

### Tipo Number

* Números enteros y reales de cualquier precisión. 
* Literal (como en Java pero sin notación octal o hexadecimal)
* Inmutable (como en Java)
* El valor NaN se usa cuando no se puede realizar una operación (como en Java)

### Tipo string

* Entre comillas simples o comillas dobles
* Como no hay tipo caracter, se usan strings con un caracter.
* Propiedad .length (como en Java)
* Operador + (como en Java)
* Inmutables (como en Java)
* Caracteres especiales y unicode (como en Java)

### Tipo boolean

* boolean: true o false.
* Inmutable (como en Java)

## Variables

* Es un lenguaje con tipado dinámico
* Las variables se tienen que declarar pero no se indica el tipo. Se infiere del valor asignado

{% highlight javascript %}
   //La variable edad tendrá un valor de 34
   var edad = 34;
   var encontrado = false;
{% endhighlight %}

* Las declaraciones se suelen hacer al principio de la función.
* La variable tiene como ámbito la función, no el bloque. Al finalizar el bloque, la variable sigue presente (En Java es por bloque).
* Regla de estilo: empieza minúsculas y separa con _ (en Java se separa con Mayúsculas).
* Si no se inicializan, las variables tienen el valor `undefined` (no `null`)
* No existe final para declarar constantes

## Operadores en expresiones

* Similares a Java
  * Aritméticos: + - * / % (a división es siempre real)
  * Comparación números: < > <= >=
  * Lógicos: && || !
  * Comparativo: ?: (Elvis operator)
  * Modificación: ++ --
  * Asignación: = += -= *= /= %=
* Diferentes a Java
  * Comparación: 
    * Igual: === 
    * Distinto: !==
    * En strings se comporta como equals en Java
    * En arrays se comporta como == en Java

## Tratamiento de valores undefined

* Si una expresión se evalúe como undefined se puede usar el operador || para devolver otro valor:

{% highlight javascript %}
    var fligth = {};
    var status = flight.status || "unknown";
    console.log(status); //Imprime "unknown"
{% endhighlight %}

* Si queremos acceder a un atributo que puede no estar definido (lo que provocaría un TypeError) se puede usar el operador && para acceder sólo si existe:

{% highlight javascript %}
    var fligth = {};
    var char = flight.status && flight.status.charAt(0);
    console.log(char); //Imprime "undefined"
{% endhighlight %}

* Se tiene este comportamiento porque los operadores lógicos en realidad se definen así:
  * Operador OR ||: Devuelve el primer operando si no tiene un valor que se interprete como falso. En otro caso devuelve el segundo operando. Como undefined se interpreta como falso, se devuelve el segundo operando en caso de que el primero evalúe como undefined. Hay que tener cuidado porque 0 y "" también se interpretan como falso.
  * Operador AND &&: Devuelve el primer operando si tiene un valor que se interprete como falso. En otro caso devuelve el segundo operando. Como undefined se interpreta como falso, se devuelve undefined en caso de que el primero evalúe como undefined. Hay que tener cuidado porque 0 y "" también se interpretan como falso.

# Arrays

## Igual que en Java

  * El acceso para lectura o escritura es con [ ]
  * Tienen la propiedad length
  * Empiezan por 0
  * La asignación no copia, las variables apuntan al mismo objeto
  * El operador === compara si son el mismo objeto (no el mismo contenido)
  * Los arrays de varias dimensiones son arrays de arrays. Hay que crear de forma explícita los niveles.

## Diferente a Java
  * Los literales son con [ ] en vez de { }
  * No se pone new en el literal

{% highlight javascript %}
var empty = [];
var numbers = ['zero','one','two','three']                
{% endhighlight %}

   * Los arrays pueden mezclar valores de varios tipos.

## Errores de acceso
  * El acceso a un elemento fuera de los límites es `undefined`
  * El intento de acceso a un array undefined da un error `TypeError`

## Gestión como listas
  * Se pueden establecer elementos en posiciones no existentes y el array crece dinámicamente. 
  * El método push es igual que add en Java.
  * La propiedad length se puede cambiar para reducir el tamaño del array.
  * El operador delete borra un elemento (pero deja el hueco)

{% highlight javascript %}
delete numbers[2];
{% endhighlight %}

  * Para borrar y no dejar el hueco se usa el método splice indicando el índice desde el que hay que borrar y el número de elementos.

{% highlight javascript %}
numbers.splice(2, 1);
{% endhighlight %}

# Sentencias de control de flujo

## Bloque de sentencias

  * Con { } como en Java
  * Las variables no desaparecen al terminar el bloque (diferente a Java).

## Sentencia if

  * Sintaxis como en Java
  * La expresión no tiene que ser booleana
  * Se interpreta como falso: 
    * false, null, undefined, '' (cadena vacía), 0, NaN

## Setencias switch, while y do
  
  * Sintaxis y semántica como en Java

## Sentencia for

  * for(init; expr; inc) como en Java. La variable de control tiene que declararse fuera del bucle.
  * No tiene continue, pero si break como en Java.

## Sentencias return y break
  * Como en Java.
  * Con soporte de etiquetas como en Java.

# Funciones

* JavaScript es un lenguaje funcional en el sentido de que las funciones son ciudadanos de primera clase en el lenguaje.
* Se pueden declarar con un nombre:

{% highlight javascript %}
  function f(param){
     console.log(param);     
  }

  f(4); // Imprime 4
{% endhighlight %}

* También se pueden declarar funciones anónimas y asignarse a una variable. Posteriormente se usa el nombre de la variable para invocar la función:

{% highlight javascript %}
  var func = function(param){
     console.log(param);     
  };

  func(4); // Imprime '4'
{% endhighlight %}

* Las funciones son en realidad objetos, así que se pueden guardar en variables (como se ha visto en el ejemplo) o se pueden pasar como parámetros a otras funciones. En Java se puede obtener una funcionalidad similar con las clases anónimas o con los lambdas de Java 8.

## Invocación de una función

* Para invocar una función se indica su nombre seguido de una lista de expresiones entre paréntesis.
* Normalmente se pasan tantas expresiones como parámetros se hayan declarado.
* Si hay menos parámetros de los definidos en la cabecera de la función, los que faltan tendrán un valor undefined.
* Si hay más valores, se ignoran (aunque se pueden obtener de forma reflectiva como se verá en la sección de reflexión).

## Información accesible desde la función

* Desde una función se tiene acceso a los parámetros y a las variables declaradas en dicha función.

{% highlight javascript %}
  var func = function (param){
     var numero = 0;
     console.log(param+" numero:"+numero);
  }

  func(4); // Imprime '4 numero:0'
{% endhighlight %}

* También se tiene acceso a variables accesibles en el ámbito en el que se declara la función:

{% highlight javascript %}
  var texto = "Hola";
  var print_texto = function (){
     console.log(texto);
  }

  print_texto(); // Imprime 'Hola'
{% endhighlight %}

* Cuando se referencia a una variable no se accede a su valor en el momento de la declaración, si no a la propia variable en sí. El conjunto de variables a las que tiene acceso la función se llama cerradura o cierre (closure). Esto tiene algunos efectos como los siguientes:

{% highlight javascript %}
  var texto = "Hola";
  var print_texto = function (){
     console.log(texto);
  }

  print_texto(); // Imprime 'Hola'
  texto = "Adios";
  print_texto(); // Imprime 'Adios'
{% endhighlight %}

* Las funciones se pueden declarar dentro de otras funciones:

{% highlight javascript %}
  var add_onclick_handler = function (node) {
      node.onclick = function (e) {
          alert("Alerta");
      };      
  };
{% endhighlight %}

* En Java, una clase anónima o una expresión lambda pueden acceder a las varibles accesibles en el ámbito sólo si las variables no cambian de valor. Esto se debe a que en Java se accede al valor, no a la variable. Y para evitar confusiones, el programador está obligado a que la variable no cambie de valor.
* El acceso a las variables del contexto tiene que utilizarse con ciudado. En el siguiente ejemplo se puede ver un uso erróneo de una variable del contexto:

{% highlight javascript %}
   //La siguiente función asocia un gestor de eventos a cada 
   //uno de los nodos que muestra una alerta. La alerta debería 
   //mostrar el número de cada nodo, pero todas muestran el número total
   //de nodos, que es el valor que toma la variable al final del bucle.
   var add_onclick_handlers = function (nodes) {
      var i;
      for (i = 0; i < nodes.length; i += 1) {
         nodes[i].onclick = function (e) {
            alert(i);
         };
      }
   };
{% endhighlight %}

* Para solucionar este problema, se podría intentar crear una variable local al cuerpo del for que tome el valor de la variable i. Pero también es errónea porque en JavaScript los bloques no definen el ámbito léxico de las variables. En Java este enfoque funciona porque el ámbito de las variables viene definido por los bloques.

{% highlight javascript %}
   //En realidad sólo existe una variable num para 
   //toda la función. 
   var add_onclick_handlers = function (nodes) {
      var i;
      for (i = 0; i < nodes.length; i += 1) {
         var num = i;
         nodes[i].onclick = function (e) {
            alert(num);
         };
      }
   }; 
{% endhighlight %}

* Para que cada nodo tenga su propio número de nodo es necesario crear un ámbito por cada nodo. Es decir, es necesario crear una función para capturar en un parámetro el valor de i en cada iteración. Luego ejecutamos dicha función y el valor devuelto es la función que realmente asociamos a la propiedad onclick del nodo:

{% highlight javascript %}
   var add_the_handlers = function (nodes) {
      var i;
      for (i = 0; i < nodes.length; i += 1) {
         nodes[i].onclick = function (i) {
            return function (e) {
               alert(e);
            };
         }(i);
      }
   };
{% endhighlight %}

# Orientación a objetos

* Los objetos se manejan mediante referencias como en Java
* Asignación no copia el objeto, copia la referencia.
* Comparación con === dice si son el mismo objeto, no si son iguales.
* Crear un objeto nuevo (como en Java):

{% highlight javascript %}
   var persona = new Object();
{% endhighlight %}

## Atributos

* También se pueden crear objetos de forma literal con los atributos (y sus valores):

{% highlight javascript %}
   var persona = {
     nombre : "Pepe",
     apellido : "García"
   };
{% endhighlight %}

* Incluso se puede crear un objeto sin atributos usando la misma notación:

{% highlight javascript %}
   var persona = {};  // Equivale a new Object();
{% endhighlight %}

* Los atributos son accesible desde cualquier parte del programa (atributos públicos en Java).
* Se accede a los atributos con la notación punto (como en Java):

{% highlight javascript %}
   persona.nombre = "Juan";
{% endhighlight %}

* Si se intenta leer de un atributo que no existe se devuelve undefined (no hay error de ejecución).

* A los objetos se les puede añadir atributos nuevos en tiempo de ejecución (en Java no se puede).

{% highlight javascript %}
   var persona = new Object();
   persona.nombre = "Pepe";
   persona.apellido = "García";
{% endhighlight %}

* También se pueden quitar atributos en tiempo de ejecucion con el operador delete:

{% highlight javascript %}
   delete persona.apellido;
{% endhighlight %}

## Métodos

* Los métodos son funciones que se asocian a los objetos:

{% highlight javascript %}
   persona.nombre_completo = function () {
     return this.nombre + " " + this.apellido;
   };
{% endhighlight %}

* También se pueden asociar al crear el objeto con la notación literal:   

{% highlight javascript %}
   var persona = {
     nombre : "Pepe",
     apellido : "García",
     nombre_completo : function () {
       return this.nombre + " " + this.apellido;
     }
   };
{% endhighlight %}

* Para invocar un método de un objeto se usa la notación punto y los parámetros entre paréntesis (como en Java).

{% highlight javascript %}
   console.log( persona.nombreCompleto() );
{% endhighlight %}

* Cuando una función se usa como un método (y se invoca con la notación punto) se puede usar la variable implícita this. Este variable apunta al objeto sobre el que se invoca el método (como en Java).
* Como en los atributos, se pueden quitar métodos con el operador delete:

{% highlight javascript %}
   delete persona.nombre_completo;
{% endhighlight %}

* Como los tipos básicos y los arrays son objetos, también se pueden usar métodos en ellos:

{% highlight javascript %}
   false.toString(); // 'false'
   [1, 2, 3].toString(); // '1,2,3'
{% endhighlight %}

* Pero en los números no se puede usar la notación punto directamente:

{% highlight javascript %}
   2.toString(); // genera SyntaxError
{% endhighlight %}

* Hay que usar alguna de las formas:

{% highlight javascript %}
   2..toString(); // the second point is correctly recognized
   2 .toString(); // note the space left to the dot
   (2).toString(); // 2 is evaluated first
{% endhighlight %}

* A los atributos y los métodos se les conoce como "propiedades" del objeto.

## Clases como objetos prototipo

* En JavaScript la programación orientada a objetos se puede está basada en prototipos. En Java está basada en el modelo "clásico" con clases.
* En vez de tener una clase que define los atributos y métodos de los objetos de esa clase, se tiene un "objeto prototipo" al que se asocian otros objetos.
* Por tanto, el concepto de clase en JavaScript se representa como un objeto que hace de prototipo de los demás objetos que se asocian a él.
* Atributos:
  * Cuando se accede a un atributo en un objeto y no existe en dicho objeto, se busca en su prototipo y se devuelve su valor.
  * Cuando se escribe en un atributo, si no existe el atributo se crea en el objeto. Por tanto el valor se cambia en el objeto, no en el prototipo.
* Métodos:
  * Cuando se intenta ejecutar un método en un objeto y no existe en dicho objeto, se busca en su prototipo y se ejecuta.
* Aunque se pueden añadir atributos y métodos a cualquier objeto (al crear el objeto o en cualquier momento posterior), se usan prototipos para reducir la memoria usada por los objetos porque usan los métodos del prototipo. También se ahorra memoria porque los atributos son los del prototipo hasta que se escribe en ellos.
* A un objeto se le pueden añadir y quitar atributos y métodos en tiempo de ejecución, pero no puede cambiar de clase (es decir, [no se puede cambiar el objeto prototipo][NoCambioPrototipo]).
* Los objetos pertenecen a una clase por el prototipo al que se asocian al crearse.
* Los objetos creados con `new Object()` o con notación JSON se asocian al prototipo `Object.prototype`. Es como decir que son instancias de la clase Object.
* Para asociar un objeto a un prototipo diferente de `Object.prototype` basta con crear una nueva función y llamarla con el operador `new`:

{% highlight javascript %}
   function Empleado(){};
   
   var empleado1 = new Empleado();
   var empleado2 = new Empleado();
{% endhighlight %}

* Una función diseñada para ser llamada con new se llama "constructor". Como regla de estilo se diferencia de las demás porque empieza por mayúsculas.
* Es muy importante poner new antes de llamar al constructor. Si no se pone new, no se producirá ningún error al analizar el código ni tampoco en ejecución, pero el comportamiento obtenido será muy raro (se explicará más adelante).
* Se puede acceder al objeto prototipo del constructor Empleado con:

{% highlight javascript %}
   Empleado.prototype;
{% endhighlight %}

* Se pueden añadir métodos y atributos a todos los empleados si se modifica el prototipo:

{% highlight javascript %}
   Empleado.prototype.nombre = "Empleado genérico";
   Empleado.prototype.salario = 600;
{% endhighlight %}

* De esa forma, todos los empleados tendrán nombre y salario:

{% highlight javascript %}
   console.log(empleado1.salario); // Imprime 600
   console.log(empleado2.salario); // Imprime 600
{% endhighlight %}

* Si cambiamos el salario a un empleado, el otro no se verá afectado:

{% highlight javascript %}
   empleado1.salario = 700;
   console.log(empleado1.salario); // Imprime 700
   console.log(empleado2.salario); // Imprime 600
{% endhighlight %}

* También se pueden añadir métodos al prototipo:

{% highlight javascript %}
   Empleado.prototype.println = function (){
     console.log("Nombre: "+this.nombre);
     console.log("Salario: "+this.salario);
   };

   empleado1.nombre = "Pepe";
   empleado1.println(); // Imprime Nombre:Pepe Salario:700
{% endhighlight %}

* Pese a la naturaleza dinámica de JavaScript, si no se necesita añadir atributos y métodos en tiempo de ejecución, se puede especificar toda la clase junta:

{% highlight javascript %}
   function Empleado2() { };
   
   //Atributos
   Empleado2.prototype.nombre = "Empleado genérico";
   Empleado2.prototype.salario = 600;

   //Métodos
   Empleado2.prototype.println = function(){
      console.log("Nombre: "+this.nombre);
      console.log("Salario: "+this.salario);
   };

   //Uso del objeto
   var empleado = new Empleado2();
   empleado.nombre = "Pepe";
   empleado.println();
{% endhighlight %}

* Se puede usar también un constructor con parámetros (y usar this en el constructor):

{% highlight javascript %}
   function Empleado3(nombre) { 
      this.nombre = nombre;
   };

   //Atributos
   Empleado3.prototype.nombre = "Empleado genérico"; 
   Empleado3.prototype.salario = 600;
 
   //Métodos
   Empleado3.prototype.println = function(){
      console.log("Nombre: "+this.nombre);
      console.log("Salario: "+this.salario);
   };

   //Uso del objeto
   var empleado = new Empleado3();
   empleado.nombre = "Pepe";
   empleado.println();
{% endhighlight %}

  Pero en este caso, no tendría mucho sentido crear el atributo `nombre` en el prototipo, ya que todos los objetos de la clase empleado se crearían con el constructor y en este se crea un atributo por cada objeto.

* Como se ha visto, también se puede usar this en el constructor (como en Java).

* Uno puede usar una sintaxis más compacta como la siguiente:

{% highlight javascript %}
   function Empleado4(){

      //Atributos
      this.nombre = "Empleado genérico";
      this.salario = 600;

      //Métodos
      this.println = function(){
         console.log("Nombre: "+this.nombre);
         console.log("Salario: "+this.salario);
      };
   }

   //Uso del objeto
   var empleado = new Empleado4();
   empleado.nombre = "Pepe";
   empleado.println();
{% endhighlight %}

  Pero en este caso, ni los atributos ni los métodos se asocian al prototipo, se asocian al nuevo objeto que se acaba de crear. Esto no es una mala práctica, simplemente conviene saber el impacto que puede tener en el consumo de memoria. El programador puede usar cualquiera de los enfoques.

* En algunos casos se puede usar el prototipo para los métodos y el objeto para los atributos:

{% highlight javascript %}
   //Atributos
   function Empleado5(){
      this.nombre = "Empleado genérico";
      this.salario = 600;
   }

   //Métodos
   Empleado5.prototype.println = function(){
      console.log("Nombre: "+this.nombre);
      console.log("Salario: "+this.salario);
   };

   //Uso del objeto
   var empleado = new Empleado5();
   empleado.nombre = "Pepe";
   empleado.println();   
{% endhighlight %}

* El problema con los enfoques vistos hasta ahora es los atributos de los objetos son públicos. Esa falta de encapsulación y abstracción puede hacer que nuestro código sea dificil de mantener porque haya otras partes del código que accedan directamente a los atributos. 

[NoCambioPrototipo]: http://stackoverflow.com/questions/7015693/how-to-set-the-prototype-of-a-javascript-object-that-has-already-been-instantiat

## Clases basadas en funciones

* Para evitar los problemas de las clases basadas en prototipos se puede usar la técnica funcional. Con esta técnica, se utiliza la capacidad de las funciones de acceder a las variables que están en el ámbito en el que se declaran (se verá más en detalle después).

{% highlight javascript %}
   function newEmpleado6(){

      //Atributos
      var nombre = "Empleado genérico";
      var salario = 600;
      
      //Métodos
      var println = function(){
         console.log("Nombre: "+nombre);
         console.log("Salario: "+salario);
      };
      
      var set_nombre = function(_nombre){
          nombre = _nombre;
      };
      
      var set_salario = function(_salario){
          salario = _salario;
      };
      
      //Código encapsulación
      var that = {};
      that.set_nombre = set_nombre;
      that.set_salario = set_salario;
      that.println = println;      
      return that;
   }

   //Uso del objeto
   var empleado6 = newEmpleado6();
   empleado6.set_nombre("Pepe");
   empleado6.set_salario(750);
   empleado6.println();
{% endhighlight %}

 * La ventaja de este enfoque es que los atributos son privados. Se pueden declarar métodos privados. Además, si un usuario del objeto modifica los métodos de este objeto, sólo afectará a los clientes del objeto, no a los métodos internos de la propia clase. Como parte negativa, este enfoque consume más memoria porque todo se declara en el objeto que se acaba de crear. El prototipo de este objeto es `Object.prototype`.
 * Hay que notar que la función `newEmpleado6` no es un constructor, por eso no está en mayúsculas y o se usa con `new`.
 * Cuando se usa el ámbito de una función para encapsula información se dice que se usa el patrón módulo (Module patter).

# Herencia

* La herencia se usa para crear una jerarquía de clasificación por especialización/generalización.
* También para reutilizar código de la clase padre en las clases hijas.
* Dependiendo se si hemos usado el enfoque basado en prototipos o el enfoque funcional, la herencia se implementa de una forma u otra.

### Herencia con clases basadas en prototipos

* Para hacer que una clase herede de otra en un sistema basado en prototipos, lo único que hay que hacer es que el prototipo sea un objeto de "clase padre". 
* Supongamos la clase Jefe5 (representada con el constructor Jefe5):

{% highlight javascript %}
   //Atributos
   function Jefe5() {
       this.despacho = "Sin asignar";
   }

   //Herencia
   Jefe5.prototype = new Empleado5();

   //Métodos
   Jefe5.prototype.printDespacho = function(){
       console.log("Despacho: "+this.despacho);
   };
   
   //Uso del objeto
   var jefe5 = new Jefe5();
   jefe5.nombre = "Antonio";
   jefe5.despacho = "D333";
   jefe5.println();
   jefe5.printDespacho();
{% endhighlight %}

  Para cambiar el prototipo que tendrán los objetos creados con un constructor es necesario cambiar el prototipo asociado antes de crear un objeto con ese constructor. En el ejemplo es la línea:

{% highlight javascript %}
    Jefe5.prototype = new Empleado5();
{% endhighlight %}

  Para más información sobre este tipo de herencia, conviene echar un vistazo a esta [documentación de Mozilla][HerenciaJSMozilla].

[HerenciaJSMozilla]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Details_of_the_Object_Model


## Herencia con clases basadas en funciones

* La herencia en este caso se hace usando el objeto de la clase padre para incializar el objeto that que se usará en la definición de la clase hija:

{% highlight javascript %}
   function newJefe6() {
       
       //Atributos
       var despacho = "Sin asignar";
              
       //Métodos
       var printDespacho = function(){
           console.log("Despacho: "+despacho);
       };
       
       var set_despacho = function(_despacho){
           despacho = _despacho;
       };
   
       //Herencia
       var that = newEmpleado6();

       //Código encapsulación
       that.printDespacho = printDespacho;
       that.set_despacho = set_despacho;
       return that;
   }
   
   //Uso del objeto
   var jefe6 = newJefe6();
   jefe6.set_nombre("Antonio");
   jefe6.set_despacho("D333");
   jefe6.println();
   jefe6.printDespacho();
{% endhighlight %}

## Acceso a atributos o métodos de la clase padre

* Clases basadas en prototipos: 
   * Basta con acceder directamente al atributo en el objeto
   * El lenguaje se encarga de buscar el atributo o método en la cadena de prototipos (jerarquía de herencia).
 
* Clases basadas en funciones: 
   * Si la propiedad tiene método de acceso público, con el método de acceso.
   * Si no, hay que hacer una función de acceso utilizada por las clases hijas.
   * Esa función de acceso tiene que guardarse en un objeto interno que se utiliza para la comunicación entre los métodos de la jerarquía de herencia (objeto my).

## Redefinición de métodos

* Basta con crear la nueva función y asignarla al objeto que se está creando para que se use esa en vez de la heredada.
* Clases basadas en prototipos: El método redefinido será usado por cualquiera que usara ese método (clientes e implementación de la clase).
* Clases basadas en funciones: El método redefinido será usado únicamente por los clientes y la implementación de las clases hijas).

super para métodos:

## Reutilización de constructores

* Clases basadas en prototipos: Creando el objeto prototipo.
* Clases basadas en funciones: Creando el objeto that.

## Reutilización de código basada en prototipos

* En vez de crear jerarquías de herencia como clases hija y clases padre, se pueden crear relaciones entre objetos de forma más flexible.
* Se puede crear un objeto simplemente indicando el objeto que actuará como prototipo, sin necesidad de usar un constructor.

{% highlight javascript %}
  var objetoProt = {
     att1: value1;
     att2: value2;
  };

  var objeto = Object.create(objetoProt);
  objeto.att3 = value3;
  objeto.att4 = value4;
{% endhighlight %}

## Polimorfismo

* Se comporta como en Java.
* En JavaScript cualquier variable puede tener como valor cualquier objeto de cualquier tipo (en Java únicamente si la variable se declara con la clase del objeto o una clase padre).
* Como las variables no tienen tipo cuando se declaran, los métodos ejecutados en una variable serán siempre los métodos del objeto que exista en ese momento.

# Funciones y objetos (la variable this)

* La variable implícita this toma diferentes valores dependiendo de cómo se invoque la función que usa this.
* Existen 4 formas de invocar una función en JavaScript:
  * Constructor Invocation Pattern
  * Method Invocation Pattern
  * Function Invocation Pattern
  * Apply Invocation Pattern
* A continuación se describe cada patrón y el significado de this.

## Constructor Invocation Pattern
    
 * Se usa cuando una función se invoca como constructor (con el operador new)
 * `this` apunta al objeto que se está creando.

{% highlight javascript %}
   function Cuadrado(lado) { 
      this.lado = lado;
      this.area = function(){
         return this.lado * this.lado;
      };
   };

   //Constructor invocation pattern
   var cuad = new Cuadrado(3);
{% endhighlight %}

## Method Invocation Pattern

 * Cuando una función se invoca como un método de un objeto (con la notación punto)
 * `this` apunta al objeto en el que se invoca el método.

{% highlight javascript %}
   function Cuadrado(lado) { 
      this.lado = lado;
      this.area = function(){
         return this.lado * this.lado;
      };
   };

   //Constructor invocation pattern
   var cuad = new Cuadrado(3);

   //Method invocation pattern
   console.log(cuad.area()); // Imprime 9
{% endhighlight %}

## Function Invocation Pattern

 * Cuando una función se invoca de forma independiente a un objeto (usando su nombre).

{% highlight javascript %}
   var suma = function (num1, num2){
      return num1 + num2;
   }

   console.log( suma(3,6) );  //Imprime 9
{% endhighlight %}

 * `this` apunta a un objeto global que existe en JavaScript.* Esto puede ser muy confuso en ciertos contextos. Por ejemplo, cuando se olvida poner el `new` al invocar un constructor, en realidad se invoca una función normal. La variable this se refiere al objeto global de JavaScript y se devuelve 'undefined'.

{% highlight javascript %}
   var cuad2 = Rectangulo(3);
   console.log(cuad2.area()); // TypeError porque cuad2 es undefined
{% endhighlight %}

 * Por ejemplo, si declaramos una función dentro de un método de un objeto y la función usa `this`, no accede al objeto en el que se declara (aunque en el ámbito en el que se encuentra this apunta a dicho objeto):

{% highlight javascript %}
    //El siguiente código no funciona porque this apunta 
    //al objeto global en JavaScript en vez de al objeto 
    //en el que se ejecuta el método.
    var pelicula = new Pelicula();
    pelicula.titulo = "Borat";
    pelicula.add_onclick_handler = function (node) {
       node.onclick = function (e) {
          alert("Película:"+this.pelicula);
       };      
    };
{% endhighlight %}

 * Para solucionar este problema se define una variable llamada `that` y se asigna a `this`:

{% highlight javascript %}
    //El siguiente código si funciona porque that apunta 
    //al objeto en el que se ejecuta el método.
    var pelicula = new Pelicula();
    pelicula.titulo = "Borat";
    pelicula.add_onclick_handler = function (node) {
       var that = this;
       node.onclick = function (e) {
          alert("Película:"+that.pelicula);
       };      
    };
{% endhighlight %}

## Apply Invocation Pattern

 * Este patron se utiliza cuando las funciones se utilizan como objetos.
 * Es una forma de reflexión porque permite tratar a las funciones de forma genérica de forma independiente a su nombre y número de parámetros.
 * Para invocar una función se invoca un método en la propia función con la notación punto. el método apply Se usan de la siguiente forma:
 
 {% highlight javascript %}
   var suma = function (num1, num2){
      return num1 + num2;
   }

   //Function invocation pattern
   var resultado = suma(3,6) 

   //Apply invocation pattern
   var resultado2 = suma.apply(null,[3,6]);
{% endhighlight %}

 * El primer parámetro de apply es el valor que tomará la variable implícita this al ejecutar la función. 
 * El segundo valor de apply es un array con los parámetros que pasar a la función.
 * Cuando la función no usa `this`, se puede pasar `null`.
 * Cuando la función utiliza `this`, hay que pasar un objeto.

{% highlight javascript %}
   function Cuadrado(lado) { 
      this.lado = lado;
      this.area = function(){
         return this.lado * this.lado;
      };
   };

   //Constructor invocation pattern
   var cuad = new Cuadrado(3);

   //Method invocation pattern
   console.log( cuad.area() ); // Imprime 9

   var areaObj = cuad.area;

   //Apply invocation pattern
   console.log( areaObj.apply(cuad) );
{% endhighlight %}

# Excepciones

* Las excepciones son conceptualmente igual que en Java.
* Existe un bloque `try {} catch(e) {} finally {}` como en Java.

{% highlight javascript %}
   try {
      var error = ...;
      if (error) {
         throw "An error";
      }
      return true;
    } catch (e) {
      alert (e);
      return false;
    } finally {
      //do cleanup, etc here
    }
{% endhighlight %}
      
* El operador throw puede lanzar como excepción un valor de tipo string, number, boolean o un objeto. 
* Lo recomendable es devolver un objeto con atributos name y message.

# Reflexión

* La reflexión es una técnica de programación que permite tratar a los objetos como si fueran valores. 
* En ciertos contextos se conoce como "meta-programación"
* Con la reflexión se puede inspeccionar a los elementos del lenguaje para conocer más información sobre ellos antes de realizar una tarea.
* La reflexión se considera una técnica avanzada de programación y en general existen formas más sencillas y directas de implementar un programa.

## Reflexión en valores

### Operador typeof

* Operador prefijo que devuelve el tipo de un valor
* Conceptualmente similar a .class de los objetos en Java
* Devuelve el tipo como uno de los strings: 'number', 'string', 'object', 'function', 'undefined', 'boolean'. En un navegador también puede devolver 'xml'.
* [Más información sobre typeof][typeof].
* Por ejemplo, para ejecutar un código si un valor es de tipo 'string':

{% highlight javascript %}
   if(typeof variable === 'string'){
      //...
   }
{% endhighlight %}

[typeof]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof

## Reflexión en objetos

### Conocer el tipo de un objeto

* Es un operador infijo que compara un valor con un constructor para saber si esa función se utilizó para crear el objeto o uno de sus prototipos.
* Conceptualmente similar al instanceof de Java

{% highlight javascript %}
   function Empleado() {}
   function Jefe() {}
   Jefe.prototype = new Empleado();
   
   new Jefe() instanceof Jefe; // true
   new Jefe() instanceof Empleado; // true
{% endhighlight %}
   
### Acceso a las propiedades de un objeto

* Se puede recorrer la lista de propiedades de un objeto (atributos y métodos) para poder tratar objetos de forma genérica:

{% highlight javascript %}
   for(var propiedad in objeto){
      console.log(propiedad+": "+objeto[propiedad]);
   }
{% endhighlight %}

* Usando typeof se puede acceder sólo a los atributos, no a los métodos. 

{% highlight javascript %}
   for(var propiedad in objeto){
       var valorPropiedad = objeto[propiedad];
       if(typeof valorPropiedad !== 'function'){
          console.log(propiedad+": "+valorPropiedad);
       };
   }
{% endhighlight %}

* Se puede determinar si una propiedad está en el objeto o en su cadena de prototipos:

{% highlight javascript %}
   for(var propiedad in objeto){
       if(objeto.hasOwnProperty(propiedad))
          var valorPropiedad = objeto[propiedad];
          //...
       }
   }
{% endhighlight %}

### Obtener el prototipo de un objeto

* Todos los objetos tienen un prototipo.
* Se puede acceder a él con el método:

{% highlight javascript %}
   var objeto = new Object();
   var prototipo_obj = Object.getPrototypeOf(objeto);
{% endhighlight %}

## Reflexión en funciones

* Independientemente de los parámetros que tenga declarados, una función puede acceder a los parámetros con los que se ha invocado de forma genérica. 
* Toda función tiene un parámetro implícito llamado `arguments` que contiene los valores con los que se ha invocado:

{% highlight javascript %}
   var sum = function ( ) {
      var i, sum = 0;
      for (i = 0; i < arguments.length; i++) {
         sum += arguments[i];
      }
      return sum;
   };
{% endhighlight %}

* Como `arguments` no es realmente un array, no tiene métodos. Para usar métodos de un array en `arguments` se puede usar este patrón:

{% highlight javascript %}
   var slice = Array.prototype.slice;
   var arrayArgs = slice.apply(arguments);
{% endhighlight %}

# Métodos de tipos básicos y arrays

* Existe una librería estándar en forma de métodos de los valores de tipos básicos. Se verá en otra entrada del blog.

<div id="note">
{% capture myinclude %}{% include vtf.markdown %}{% endcapture %}
{{ myinclude | markdownify }}
</div>