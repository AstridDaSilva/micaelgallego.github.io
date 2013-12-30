---
layout: post
title: Orientación a Objetos en JavaScript comparado con Java (VTF3)
category: front-end
tags: javascript, poo
year: 2013
month: 12
day: 30
published: true
summary: En esta entrada intento aprender cual es la mejor forma de usar la orientación a objetos en JavaScript. Pero todavía no lo tengo claro. ¿Me echas una mano?
image: viaje-front-end/JavaScript-logo.png
---

Esta es mi tercera entrada en la serie de posts **Viaje por las tecnologías de Front-end**. Si tienes interés, puedes echar un vistazo a la [Parte 1][] y la [Parte 2][].

[Parte 1]: /blog/Viaje-por-las-tecnologias-de-front-end
[Parte 2]: /blog/Viaje-por-las-tecnologias-de-front-end2

Yo soy desarrollador Java hace más de 10 años. Aprendí programación orientada a objetos en la universidad (EUI-UPM) de la mano de Luis Fernández, uno de los mejores profesores que he tenido. Era una época en la que la orientación a objetos no era _main stream_ y costaba mucho encontrar material de calidad sobre el tema. Había muchos desarrolladores que no sabían utilizar de forma adecuada la orientación a objetos. De hecho, leyendo libros como [Effective Java Programming][] te das cuenta de que hace 15 años incluso los mejores ingenieros no tenían claros algunos aspectos de la programación orientada a objetos (clases Date, Stack, etc...). Afortunadamente, creo que ahora hay un consenso generalizado sobre utilizar de forma adecuada la orientación a objetos para desarrollar programas modulares y legibles, lo que favorece su desarrollo y mantenimiento.

[Effective Java Programming]: http://www.amazon.com/Effective-Java-Edition-Joshua-Bloch/dp/0321356683

Partiendo de ese _background_, una de las cosas que menos me gusta de JavaScript es que no hay un consenso sobre la mejor forma de implementar la orientación a objetos. Sobre todo en las jerarquías de herencia. De hecho, hay algunos desarrolladores (como el autor del libro [JavaScript: The Good Parts][]) que indican que las jerarquías de herencia tienen mucho menos sentido en lenguajes con tipado dinámico (como JavaScript). Otro síntoma de que no hay consenso en cómo usar la orientación a objetos en JavaScript es que hay múltiples librerías que facilitan la definición de clases.

En este post he recopilado toda la información que he encontrado en fuentes fiables de Internet y en buenos libros de JavaScript sobre la orientación a objetos con JavaScript. A ver si de esa forma puedo entender cual es la mejor forma de estructurar y reutilizar código para que sea mantenible usando los principios de la orientación a objetos. 

Como supongo que ya sabes, en JavaScript hay 125 formas de conseguir que un programa se comporte de una determinada forma. Hay cierto consenso en que 75 formas no son adecuadas, pero todavía quedan otras 50 formas de hacerlo "razonable". Este post no pretende ser un repaso a todos y cada uno de los detalles que permiten tener el mismo resultado en JavaScript. Si quieres conocer esos detalles, lo mejor será que te leas 4 o 5 buenos libros ;). 

Si no tienes mucha experiencia con JavaScript (como yo), te recomiendo que eches un vistazo a mi post con una [introducción a JavaScript para programadores Java][Parte 2]. 

Para preparar este post me he basado en las siguientes páginas y libros:

* [Documentación oficial de Mozilla][Mozilla] (2010 con ajustes posteriores)
* [Patrón Módulo en JavaScript][Patrón Módulo] 
* [Página del MSDN Magazine][] (Mayo 2007)
* Libro [JavaScript: The Good Parts][GoodParts] (Mayo 2008)
* Libro [Secrets of the JS Ninja][] (2013)
* Libro [Effective JavaScript][] (Noviembre 2012)
* Libro [Eloquent JavaScript][] (Julio 2007)
* StackOverflow [How to properly create a custom object in javascript][SO1]
* StackOverflow [JavaScript Inheritance][SO2]

[Mozilla]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Details_of_the_Object_Model
[GoodParts]: http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742
[Secrets of the JS Ninja]: http://www.manning.com/resig/
[Effective JavaScript]: http://effectivejs.com/
[Patrón Módulo]: http://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript
[Página del MSDN Magazine]: http://msdn.microsoft.com/en-us/magazine/cc163419.aspx
[SO1]: http://stackoverflow.com/questions/1595611/how-to-properly-create-a-custom-object-in-javascript#1598077
[SO2]: http://stackoverflow.com/questions/7486825/javascript-inheritance
[Eloquent JavaScript]: http://eloquentjavascript.net/

# Creación de clases independientes (sin herencia)

Para que sea más sencillo de entender los diferentes modelos, primero describiré como crear una clase que no haga uso de una jerarquí de herencia. Posteriormente veremos cómo se hace herencia con cada uno de los modelos. 

## Clases en Java

Si no consideramos los métodos y atributos estáticos, una clase en Java es una descripción de los métodos y atributos que tendrán los objetos de dicha clase. Es decir, todo objeto es una instancia de una clase, que define sus métodos y sus atributos. Cada objeto tendrá valores diferentes para sus atributos, pero todos los objetos compartirán los mismos métodos.

Por ejemplo, si queremos representar empleados en un programa Java, la clase `Empleado` se definiría así:

{% highlight java %}

public class Empleado {
	
   private String nombre;
   private double salario;

   public Empleado(String nombre, double salario){
      this.nombre = nombre;
      this.salario = salario;     
   }

   public String toString(){
      return "Nombre:"+nombre+", Salario:"+salario;
   }
}
{% endhighlight %}

Y así se crearía un objeto de esa clase y se usarían sus métodos:

{% highlight java %}
Empleado empleado = new Empleado("Juan",800);
System.out.println( empleado.toString() );
{% endhighlight %}

Como se puede ver, en Java la visibilidad de los elementos es un concepto importante. La clase y sus métodos son públicos (se pueden usar desde cualquier parte del programa), mientras que los atributos son privados (sólo se pueden usar desde la implementación de la clase).

## Clases con prototipos en JavaScript

En JavaScript no existe el concepto de clase. Es decir, no existe una descripción de los métodos y los atributos que tendrá un objeto. Para que un objeto tenga atributos, basta con dar un valor inicial a una propiedad del objeto con el nombre que queramos para el atributo. Para que un objeto tenga métodos, basta con asignar a una propiedad del objeto una función. En definitiva, en JavaScript sólo hay objetos y funciones.

Para optimizar el consumo de memoria y el tiempo de ejecución, existe el concepto de prototipo. Todo objeto en JavaScript tiene asociado un objeto especial llamado "prototipo". Cuando se accede a un atributo o se invoca un método de un objeto y el objeto no tiene dicho atributo o método, se busca en su prototipo. Además, un prototipo puede tener a su vez otro prototipo, creando una "cadena de prototipos".

Aunque existen diversas formas de usar los prototipos en JavaScript, lo más aceptado es que una clase se represente de la siguiente forma:
* Los atributos se asocian al nuevo objeto en la función constructor (que crea el objeto y le asocia el prototipo).
* Los métodos se asocian al prototipo. 

Como en el lenguaje JavaScript no existen las clases, no hay consenso sobre lo que es una clase en JavaScript. Si usamos el patrón de clases con prototipos, podemos decir que una clase es su función constructor y el código que asocia los métodos al prototipo.

Siguiendo este criterio, la clase empleado se crearía: 

{% highlight javascript %}

   function Empleado(nombre, salario){
      this.nombre = nombre;
      this.salario = salario;
   }

   Empleado.prototype.getNombre = function(){
      return nombre;
   };
      
   Empleado.prototype.getSalario = function(){
      return salario;
   };

   Empleado.prototype.toString = function(){
      return "Nombre:"+this.nombre+", Salario:"+this.salario;
   };

{% endhighlight %}

Y para crear un objeto empleado y usar sus métodos: 

{% highlight javascript %}
var empleado = new Empleado("Pepe", 700);
console.log( empleado.toString() );
{% endhighlight %}

Una diferencia entre JavaScript y Java es que en JavaScript todos los atributos y métodos son accesibles desde cualquier parte del programa. En terminología de Java, todos los atributos y métodos son públicos. En realidad, la visibilidad de los elementos es una documentación que escribe el desarrollador que crea la clase y que se verifica por el compilador. El desarrollador dice que un método es privado porque no quiere que nadie use el método de forma que pueda combiarlo en el futuro si lo necesita. Eso también permite abstrar el usuario de la clase de detalles que no son relevantes para él. 

En JavaScript no hay compilador que proteja los elementos privados. Pero tampoco existen mecanismos para que se genere un error en ejecución que impida a un cliente acceder a atributos o métodos privados. Lo único que se puede hacer es documentar la clase de forma adecuada y esperar que el cliente se lea la documentación y la haga caso ;).

Pero ese no es el problema más grave. El principal problema es que en JavaScript todo es dinámico (no sólo el tipo de las variables). Cualquier código que esté utilizando un objeto puede cambiar ese objeto de forma radical en tiempo de ejecución. En concreto, puede hacer lo siguiente: 

 * Puede añadir atributos al objeto. 
 * Puede quitar atributos al objeto, incluso aquellos que se establecieron en la función constructor.
 * Puede añadir métodos al objeto.
 * Puede añadir atributos al prototipo de un objeto, haciendo que todos los objetos de esa clase (que comparten el prototipo) tengan un nuevo atributo con el mismo valor.
 * Puede añadir métodos al prototipo de un objeto, haciendo que todos los objetos de esa clase (que comparten el prototipo) tengan un nuevo método. 

Con esta extrema flexibilidad, la única forma de que el programa sea fácil de entender y por tanto de desarrollar y mantener, es leer bien la documentación y usar cada objeto como el desarrollador quiere que se use. En concreto, si no hay buenas razones para hacerlo, no se debería modificar estructuralmente un objeto ni sus prototipos. Además, no se deberá acceder directamente a los atributos de un objeto si existen métodos para hacerlo, porque eso será una señal de que esos atributos pueden ser un detalle de implementación que puede cambiar en el futuro (aka, atributos privados).

Para paliar esta extrema flexibilidad, recientemente se han añadido mecanismos para evitar que los atributos se puedan alterar una vez construido el objeto. Estos mecanismos de protección sólo se aplican si se usa el [modo estricto de JavaScript][StrictMode]. Para más información sobre estas características conviene consultar la [página oficial de Mozilla][] y el [blog del creador de jQuery][]. No obstante, no he visto la forma de utilizar estos mecanismos para crear clases más seguras. El principal problema es que los mecanismos de protección del objeto no están pensados para utilizarse en un contexto en el que hay jerarquías de herencia entre objetos. No sé, quizás esté equivocado.

[StrictMode]: http://ejohn.org/blog/ecmascript-5-strict-mode-json-and-more/
[página oficial de Mozilla]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty
[blog del creador de jQuery]: http://ejohn.org/blog/ecmascript-5-objects-and-properties/

Existen muchas variantes al código que se ha mostrado para implementar clases como prototipos. A continuación se describen algunas de ellas:

* Si no se usa el operador `new` al crear el objeto y se llama directamente a la función, no se produce ningún error en tiempo de ejecución pero ocurren muchas cosas inesperadas. En el Item 33 del [Effective JavaScript][] tienes algunos consejos para generar un error o para que se comporte de forma adecuada aunque no uses `new`. Usar estas técnicas depende de lo [defensivo][] que quieras ser programando.
* Los métodos se pueden guardar en el objeto en vez de en su prototipo con el objetivo de que la invocación del método sea más rápida (ya que se evitaría la búsqueda en el prototipo). Según comentan en [Effective JavaScript][] parece que eso podría aumentar el consumo de memoria de cada objeto y no se reduciría de forma aprecible el tiempo de ejecución porque la ejecución de métodos suele estar optimizada.

[defensivo]: http://es.wikipedia.org/wiki/Programaci%C3%B3n_defensiva
[funciones herencia clásica]: http://ejohn.org/blog/simple-javascript-inheritance/

Aunque esta es la forma original de implementar clases, los desarrolladores han ideado formas que permiten sortear los problemas que presenta este patrón.

## Clases con módulos en JavaScript

Algunos programadores consideran que es inaceptable que JavaScript no permita controlar la visibilidad de los atributos y los métodos. Para sortear el problema han usado una técnica que permite crear objetos con atributos privados y con métodos públicos y privados. Además, aunque no se evite completamente, se reducen los cambios estructurales que se le pueden hacer a un objeto.

La técnica se conoce como [Patrón Módulo] y aunque se puede aplicar en otros contextos, se utiliza para encapsular atributos y métodos de objetos. Esta técnica se basa en el hecho de que una función captura las variables que tiene a su alcance y siempre que sea llamada esa función podrá acceder a dichas variables. A esto se le conoce como _closure_. 

A continuación se presenta una clase implementada usando esta técnica:

{% highlight javascript %}

   function newEmpleado(nombre, salario){

      var that = {};

      var _nombre = nombre;
      var _salario = salario;

      function getNombre(){
          return _nombre;
      }
      
      function getSalario(){
          return _salario;
      }

      function toString(){
         return "Nombre:"+_nombre+", Salario:"+_salario;
      }   
      
      that.getNombre = getNombre;
      that.getSalario = getSalario;
      that.toString = toString;

      return that;
   }

{% endhighlight %}

Y para crear un objeto empleado y usar sus métodos: 

{% highlight javascript %}
var empleado = newEmpleado("Pepe", 700);
console.log( empleado.toString() );
{% endhighlight %}

Si analizamos el código, podemos darnos cuenta de los siguientes detalles:

* La función `newEmpleado` no se llama usando el operador `new`, por tanto, estrictamente hablando, no es un constructor.
* El nuevo objeto se crea como un objeto literal dentro de la función, por tanto su prototipo es `Object.prototype`. 
* El nuevo objeto no tiene los atributos como propiedades. Los atributos se representan como variables locales de la función `newEmpleado`. A estas variables locales tienen acceso todas las funciones que hacen de métodos del objeto porque forman parte de su closure.
* Los métodos del nuevo objeto se guardan como propiedades en el propio objeto, no en su prototipo. Esto se debe a que los métodos son específicos para ese objeto, porque tienen acceso directo a las variables que actúan como atributos. 
* En la implementación de los métodos no se utiliza el objeto implícito `this` para acceder a los atributos.

Este patrón de clases como módulos tiene las siguientes ventajas frente al patrón original de clases como prototipos:

* Los atributos son privados. Es decir, desde un código que usa el objeto no se puede modificar directamente el valor de los atributos. Tampoco se pueden borrar.
* Se pueden poner métodos privados no accesibles por los clientes del objeto. Basta con que esos métodos no se establezcan como propiedades del objeto `that`.
* No hay forma de modificar los métodos de todos los objetos de una clase porque la clase no se representa con un prototipo. Es decir, al estar todos los métodos como propiedades del propio objeto, cada objeto es independiente.

Algunos de los "puntos débiles" del patrón de clases como prototipos siguen estando presentes en el patrón de clases como módulos:

* Cualquier código que tenga acceso a un objeto, puede borrar los métodos o sustituirlos por otros. 

Además, existen algunos inconvenientes al implementar las clases como funciones:

* El consumo de memoria puede ser importante debido a que cada objeto tiene sus propios métodos (en vez de ser propiedades del objeto prototipo compartido por todos los objetos de la clase).
* El valor de los atributos no es visible en los depuradores (al menos en el de Google Chrome) porque no son propiedades del objeto.
* Este patrón requiere un poco más de código que el patrón original, lo que puede dar lugar a más complejidad en el desarrollo y mantenimiento.

## Clases con librerías en JavaScript

Como ya se ha visto, la orientación a objetos basada en prototipos de JavaScript es diferente a la orientación a objetos basada en clases de Java y otros lenguajes. No obstante, una vez que comprendes el funcionamiento de los prototipos comprendes que si te abstraes un poco, son conceptualmente muy similares. Es decir, puedes obtener esencialmente el mismo comportamiento. Pero como se ha visto en los ejemplos de código, la sintaxis para crear una clase con prototipos puede ser confusa, propensa a errores y verbosa. Además, crear jerarquías de herencia es todavía más complicado (como se verá más adelante).

Debido a todos estos aspectos, hace unos años empezaron a surgir librerías en JavaScript que permiten definir clases de forma que el código se parece a como se definen las clases en lenguajes como Java. En el libro [Secrets of the JS Ninja][] se dice que estas librerías implementan "técnicas de simulación de herencia clásica", porque donde más ayudan es en la creación de jerarquías de herencia. En el libro [JavaScript: The Good Parts][GoodParts] también se utiliza el término "herencia clásica". 

Algunas de las librerías ofrecen mucha más funcionalidad, pero aquí sólo estamos interesados en la definición de clases. A continuación se presenta la sintaxis que se usa en algunas de las librerías más relevantes y actualizadas como [Prototype.js][] y [JS.Class][]. No obstante, hay bastantes más librerías que permiten crear clases como [Base2][], [Joose][], [klass][], [Mootools][], [selfish][], [classy][], [qooxdoo][], [yui][]. 

Para comprender cómo funcionan estas librerías se pueden consultar las siguientes referencias:

* En el libro [JavaScript: The Good Parts][GoodParts] y en [esta web de su autor][HerenciaClasica].
* En el libro [Secrets of the JS Ninja][] y en [este post del autor][ClasesNinjaPost].
* En [este hilo de StackOverflow][JerarquiasJavaScript].

[Prototype.js]: http://prototypejs.org/
[JS.Class]: http://jsclass.jcoglan.com/
[Base2]: http://code.google.com/p/base2/
[Joose]: http://joose.it/
[klass]: https://github.com/ded/klass]
[HerenciaClasica]: http://javascript.crockford.com/inheritance.html
[Mootools]: http://mootools.net/docs/core/Class/Class]
[selfish]: https://github.com/Gozala/selfish
[classy]: http://classy.pocoo.org/
[qooxdoo]: http://manual.qooxdoo.org/1.4.x/pages/core/classes.html
[yui]: http://yuilibrary.com/yui/docs/yui/yui-extend.html
[JerarquiasJavaScript]: http://stackoverflow.com/questions/7486825/javascript-inheritance]

No he revisado todas las librerías, pero creo que la gran mayoría de ellas sólo introducen azucar sintáctico para crear clases con prototipos. No he visto ninguna librería que ayude a crear clases con módulos.

### Prototype.js

Con esta librería se crean clases como prototipos pero con una sintáxis inspirada en lenguajes como Java. Por ejemplo, la clase Empleado se crearía así: 

{% highlight javascript %}

var Empleado = Class.create({

   initialize: function(nombre, salario){
      this.nombre = nombre;
      this.salario = salario;
   }, 

   getNombre: function(){
      return nombre;
   },
      
   getSalario: function(){
      return salario;
   },

   toString: function(){
      return "Nombre:"+this.nombre+", Salario:"+this.salario;
   }
});
{% endhighlight %}

Y un objeto se crearía y usaría de la misma forma que las clases basadas en prototipos. Al fin y al cabo, es sólo azucar sintáctico al crear los objetos:

{% highlight javascript %}
var empleado = new Empleado("Pepe", 700);
console.log( empleado.toString() );
{% endhighlight %}

[ClasesNinjaPost]: http://ejohn.org/blog/simple-javascript-inheritance/

### JS.Class

Esta librería es relativamente reciente y pretende simular en JavaScript la forma de definir clases en Ruby. Sigue la misma filosofía que las librerías anteriores. La clase empleado definida con esta librería se implementaría:

{% highlight javascript %}

var Empleado = new Class({

   initialize: function(nombre, salario){
      this.nombre = nombre;
      this.salario = salario;
   }, 

   getNombre: function(){
      return nombre;
   },
      
   getSalario: function(){
      return salario;
   },

   toString: function(){
      return "Nombre:"+this.nombre+", Salario:"+this.salario;
   }   
});
{% endhighlight %}

Y los objetos se usarían de la misma forma que con clases basadas en prototipos:

{% highlight javascript %}
var empleado = new Empleado("Pepe", 700);
console.log( empleado.toString() );
{% endhighlight %}

# Herencia de clases

Una de las características más innovadoras de la programación orientada a objetos frente a los paradigmas de programación previos es la capacidad de implementar jerarquías de clasificación de conceptos utilizando la herencia de clases. Esta potente técnica de programación permite definir una clase ampliando otra clase previamente definida. Además, en ciertos casos, parte del comportamiento definido en la clase base se redefine para adaptarlo a las peculiaridades de las clases hijas. 

Veamos cómo se pueden implementar jerarquías de herencia en Java y en JavaScript con cada uno de los patrones de implementación de clases.

## Herencia de clases en Java

Para implementar una jerarquía de herencia en Java basta crear una clase hija que `extends` de la clase padre. Supongamos que queremos implementar una clase Jefe que herede de empleado. Vamos a añadir un atributo `despacho`. Además, vamos a redefinir el método `toString` reutilizando la implementación de `toString` de la clase padre. 

Se muestra la clase Empleado de nuevo: 

{% highlight java %}

public class Empleado {
	
   private String nombre;
   private double salario;

   public Empleado(String nombre, double salario){
      this.nombre = nombre;
      this.salario = salario;     
   }

   public String toString(){
      return "Nombre:"+nombre+", Salario:"+salario;
   }
}
{% endhighlight %}

La clase hija Jefe se implementaría: 

{% highlight java %}
public class Jefe extends Empleado {

   private String despacho;

   public Jefe(String nombre, double salario, String despacho){
      super(nombre, salario);
      this.despacho = despacho;
   }

   public String toString(){
      return super.toString()+" Despacho:"+this.despacho;
   }
}
{% endhighlight %}

Y así se crearía un objeto de esa clase y se usarían sus métodos:

{% highlight java %}
Jefe jefe = new Jefe("Pepe", 700, "E12");
System.out.println( jefe.toString() );
{% endhighlight %}

## Herencia de clases con prototipos en JavaScript

Para implementar una jerarquía de herencia con prototipos en realidad lo que hay que hacer es una cadena de prototipos. El primer elemento de la cadena será el objeto, su prototipo será el objeto de la clase hija y el prototipo de ésta será el objeto de clase padre.

Se incluye la clase Empleado de nuevo para recordar su implementación:

{% highlight javascript %}

   function Empleado(nombre, salario){
      this.nombre = nombre;
      this.salario = salario;
   }

   Empleado.prototype.getNombre = function(){
      return nombre;
   };
      
   Empleado.prototype.getSalario = function(){
      return salario;
   };

   Empleado.prototype.toString = function(){
      return "Nombre:"+this.nombre+", Salario:"+this.salario;
   };
{% endhighlight %}

La implementación de la clase Jefe sería:

{% highlight javascript %}

   function Jefe(nombre, salario, despacho){
      //Llamada al constructor padre
      Empleado.call(this, nombre, salario);
      this.despacho = despacho;
   }

   //Conexión de prototipo clase hija a clase padre
   Jefe.prototype = Object.create(Empleado.prototype);

   Jefe.prototype.toString = function(){
      //Llamada a método redefinido
      return Empleado.prototype.toString.call(this)+" Despacho:"+this.despacho;
   };
{% endhighlight %}

Y para crear un objeto jefe y usar sus métodos: 

{% highlight javascript %}
var jefe = new Jefe("Pepe", 700, "E12");
console.log( jefe.toString() );
{% endhighlight %}

Con la implementación mostrada, el objeto tiene todos sus atributos como propiedades del propio objeto. Estas propiedades se establecen en las llamadas que se hacen a los constructores de la jerarquía de herencia. A diferencia de Java, en JavaScript es necesario llamar al constructor de la clase padre de forma explícita, aunque no tenga parámetros. 

{% highlight javascript %}

   function Jefe(nombre, salario, despacho){
      //Llamada al constructor padre
      Empleado.call(this, nombre, salario);
      this.despacho = despacho;
   }
{% endhighlight %}

A diferencia de los atributos, los métodos son propiedades de los prototipos. Para crear la jerarquía de herencia hay que hacer que el prototipo de los objetos de la clase Jefe sea un objeto de la clase Empleado. Esto se consigue con la siguiente sentencia:

{% highlight javascript %}
   //Conexión de prototipo clase hija a clase padre
   Jefe.prototype = Object.create(Empleado.prototype);
{% endhighlight %}

De esta forma, cuando un método no están en un prototipo, se busca en el siguiente de la cadena. Esto optimiza el consumo de memoria y según parece la búsqueda de los métodos en la cadena de prototipos está bastante optimizada, así que no hay mucho impacto en la ejecución. 

Por último, para redefinir un método basta con asignar una nueva función en el prototipo de la clase hija que "oculta" la función del prototipo de la clase padre cuando se realiza la búsqueda. 

{% highlight javascript %}

   Jefe.prototype.toString = function(){
      return Empleado.prototype.toString.call(this)+" Despacho:"+this.despacho;
   };
{% endhighlight %}

Además, si en la implementación del método redefinido se quiere llamar al método original, basta con hacer esa llamada de forma explícita usando una referencia al protototipo de la clase padre, que es el que contiene el método.

## Herencia de clases con módulos en JavaScript

Si se implementan las clases como módulos también se pueden crear jerarquías de herencia. Como hemos hecho antes, se incluye aquí la implementación de la clase Empleado para recordar la implementación:

{% highlight javascript %}

   function newEmpleado(nombre, salario){

      var that = {};

      var _nombre = nombre;
      var _salario = salario;

      function getNombre(){
          return _nombre;
      }
      
      function getSalario(){
          return _salario;
      }

      function toString(){
         return "Nombre:"+_nombre+", Salario:"+_salario;
      }   
      
      that.getNombre = getNombre;
      that.getSalario = getSalario;
      that.toString = toString;

      return that;
   }
{% endhighlight %}

Para implementar una clase hija Jefe que añade un atributo y redefine el método toString es la siguiente:

{% highlight javascript %}

   function newJefe(nombre, salario, despacho){

      var that = newEmpleado(nombre, salarion);

      var _despacho = despacho;
      
      var super_toString = that.toString;
      function toString(){
          return super_toString()+" Despacho:"+_despacho;
      }

      that.toString = toString;

      return that;
   }
{% endhighlight %}

Como se puede ver en el código, no se manipulan los prototipos para crear la relación de herencia. Hay que recordar que cuandos se usan módulos, no se utilizan los prototipos para nada. Todos los objetos están asociados al prototipo `Object.prototype`. Es decir, el objeto creado con esta técnica tendrá como propiedades todos los atributos y métodos. 

Otro detalle que es importante notar es la llamada al método redefinido `toString`:

{% highlight javascript %}
   var super_toString = that.toString;
   function toString(){
       return super_toString()+" Despacho:"+_despacho;
   }
{% endhighlight %}

Primero se guarda una referencia al método `toString` de la clase padre de forma que pueda usarse durante las posteriores ejecuciones del método redefinido.

Para crear un objeto jefe y usar sus métodos: 

{% highlight javascript %}
   var jefe = newJefe("Pepe", 700, "E12");
   console.log( jefe.toString() );
{% endhighlight %}

## Herencia con clases con librerías en JavaScript

Las librerías de definición de clases muestran su verdadero potencial al crear jerarquías de herencia de clases. Cabe recordar que la mayoría de ellas facilitan la creación de clases como prototipos.

Las principales funcionalidades que ofrecen son:
* Azucar sintáctico para crear clases visualmente más parecidas a lenguajes como Java.
* Automatizan la configuración del objeto prototipo de la clase hija como una instancia de la clase padre.
* Automatizan la invocación del constructor de la clase padre antes de invocar el constructor de la clase hija.
* Ofrecen mecanismos sencillos para llamar a métodos redefinidos de la clase padre.

### Prototype.js

Para crear una jerarquía de herencia con Prototype.js se utiliza el siguiente patrón:

{% highlight javascript %}

var Empleado = Class.create({

   initialize: function(nombre, salario){
      this.nombre = nombre;
      this.salario = salario;
   }, 

   getNombre: function(){
      return nombre;
   },
      
   getSalario: function(){
      return salario;
   },

   toString: function(){
      return "Nombre:"+this.nombre+", Salario:"+this.salario;
   }
});

var Jefe = Class.create(Empleado, {
  
   initialize: function($super, nombre, salario, despacho){
      $super(nombre, salario);
      this.despacho = despacho;
   },

   toString: function($super) {
      return $super() + " Despacho:"+this.despacho;
   }
});
{% endhighlight %}

Como se puede apreciar, el código es bastante más limpio que crear directamente la clase hija usando cualquiera de los patrones anteriores. Una de las principales ventajas de usar esta librería es el atributo `$super` utilizado para acceder al constructor y a los métodos redefinidos de la clase padre. 

### JS.Class

En el caso de JS.Class la creación de una jerarquía de herencia es muy parecida a Prototype.JS:

{% highlight javascript %}

var Empleado = new Class({

   initialize: function(nombre, salario){
      this.nombre = nombre;
      this.salario = salario;
   }, 

   getNombre: function(){
      return nombre;
   },
      
   getSalario: function(){
      return salario;
   },

   toString: function(){
      return "Nombre:"+this.nombre+", Salario:"+this.salario;
   }   
});

var Jefe = new Class(Empleado, {

    initialize: function(nombre, salario, despacho){
      this.callSuper(nombre, salario);
      this.despacho = despacho;
    },

    toString: function() {
      return this.callSuper() + " Despacho:"+this.despacho;
    }
});
{% endhighlight %}

En este caso, el parámetro `$super` se sustituye por un método `callSuper` en el objeto que está accesible durante la ejecución de los métodos de la clase hija.

# Manipulación de clases y objetos

Cuando se utiliza la programación orientada a objetos, la mayor parte del código de un programa consiste en definir clases, crear objetos e invocar sus métodos. No obstante, también hay una serie de servicios adicionales relacionados con las clases y los objetos que también se utilizan en un lenguaje. A continuación se muestra cómo se ven afectados esos servicios adicionales cuando se usa un patrón u otro.

## Métodos como funciones independientes

En los lenguajes funcionales como JavaScript y Java 8 es bastante habitual tratar los métodos de un objeto como funciones independientes que se pasan a otras funciones. Por ejemplo, supongamos que usamos una librería en la que tenemos que establecer un _callback_, es decir, una función que será llamada cuando se produzca un determinado evento.

{% highlight javascript %}
lib.addCallback(func);
{% endhighlight %}

Si queremos pasar un método de un objeto como callback hemos de tener en cuenta el patrón elegido para implementar las clases porque esto afecta a cómo se debe pasar el método a la función.  

Si hemos usado el patrón de clases con módulos podemos usar el método directamente como callback:

{% highlight javascript %}
var empleado = newEmpleado("Antonio", 500);
lib.addCallback( empleado.toString );
{% endhighlight %}

En cambio, si hemos usado el patrón de clases con prototipos o clases con librerías, no podemos usar este enfoque. Esto se debe a que cuando se invoca un método como una función independiente la variable implícita `this` no está asociada al objeto original. En este caso, tendríamos que usar el siguiente esquema:

{% highlight javascript %}
var empleado = new Empleado("Antonio", 500);
lib.addCallback( empleado.toString.bind(empleado) );
{% endhighlight %}

Es bastante parecido, pero hay que tener en cuenta la sutil diferencia.

En Java 8 también se puede pasar un método como parámetro cuando se espera una función de la siguiente forma:

{% highlight java %}
Empleado empleado = new Empleado("Antonio", 500);
lib.addCallback( empleado::toString );
{% endhighlight %}

## Reflexión

La reflexión es un aspecto importante de un lenguaje de programación. Aunque no tengo mucha experiencia con lenguajes dinámicos, creo que la reflexión se utiliza mucho más en este tipo de lenguajes que en los lenguajes con tipado estático. Creo que eso se debe a que en los lenguajes con tipado estático la reflexión es más costosa que el uso directo de los elementos del lenguaje. En cambio, en los lenguajes dinámicos, la diferencia es menor. Además, en los lenguajes dinámicos la flexibilidad se explota mucho más que en los lenguajes con tipado estático.

En JavaScript existen diversos mecanismos para programar de forma reflexiva con la orientación a objetos, pero depende del patrón que se haya usado se podrán usar de una forma u otra. A continuación se describe cada uno de ellos:

### Saber si un valor es un objeto 

En Java el sistema de tipos está dividido en dos: tipos primitivos y objetos. Para saber si un objeto es realmente un objeto o un array, se puede usar el siguiente esquema:

{% highlight java %}
if(obj.getClass().isArray()) {
   //Es array
} else {
   //Es objeto no array
}
{% endhighlight %}

En JavaScript el operador `typeof` es un operador infijo que devuelve el tipo de un valor como un string. Cuando el valor es un objeto o un array, este operador devuelve `'object'`. Por ejemplo, para saber si un valor es un objeto o un array se usa el siguiente esquema:

{% highlight javascript %}  
   if(typeof variable === 'object'){
      if(Array.isArray(variable){
      	//Es array
      } else {
      	//Es objeto no array
      }
   } 
{% endhighlight %}

Esta técnica se puede usar con cualquiera de los patrones. Se puede consultar esta página [para más información sobre el operador typeof][typeof] y la función [isArray][].

[typeof]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof
[isArray]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray

### Saber la clase de un objeto

El operador infijo `instanceof` se usa para saber la clase de un objeto cuando se usa el patrón de clase como prototipo. Se utiliza comparando el objeto con la función constructora siguiendo el siguiente esquema:

{% highlight javascript %}
   var esJefe = new Jefe() instanceof Jefe; // true
   var esEmpleado = new Jefe() instanceof Empleado; // true
   var esRectangulo = new Jefe() instanceof Rectangulo; // false
{% endhighlight %}

Conceptualmente es similar al operador `instanceof` en Java. Además usa la misma sintáxis:

{% highlight java %}
   boolean esJefe = new Jefe() instanceof Jefe; // true
   boolean esEmpleado = new Jefe() instanceof Empleado; // true
   boolean esRectangulo = new Jefe() instanceof Rectangulo; // false
{% endhighlight %}

Hay que tener en cuenta que este operador no se puede usar con el patrón de clases con módulos. Esto se debe a que los objetos creados de esa forma son únicamente de la clase Object (ya que están asociados al prototipo `Object.prototype`).

### Acceso a la clase de un objeto

Para acceder a la clase de un objeto en Java se usa el método `getClass()`:

{% highlight javascript %}
   Empleado empleado = new Empleado();
   Class clase = empleado.getClass();
   clase.isInstance(empleado); //true
{% endhighlight %}

Cuando se usa el patrón de clases con prototipos, la clase está representada como el prototipo. En ese caso se puede consultar el prototipo de un objeto usando el método `getPrototypeOf` con el siguiente esquema:

{% highlight javascript %}
   var empleado = new Empleado();
   var prototipo = Object.getPrototypeOf(empleado);
   prototipo == Empleado.prototype // true
{% endhighlight %}

El método `getPrototypeOf()` se ha incorporado hace poco a JavaScript, pero desde hace tiempo existe una propiedad llamada `__proto__` que guarda una referencia al prototipo. Aunque en funcion en algunos casos, es mejor usar el estándar. No obstante, cuando estamos inspeccionando un objeto en el depurador, esa propiedad suele estar presente y apunta al objeto prototipo.

Al igual que ocurre con el operador `instanceof`, el método `getPrototypeOf` tampoco se puede usar con el patrón de clases como módulo porque el prototipo siempre es `Object.prototype`. 

Es decir, no podemos usar ningún mecanismo del lenguaje para conocer de forma reflexiva la clase de un objeto si usamos el patrón de clase con módulo. Como forma de solucionar el problema, siempre se podría usar un atributo que guardara el nombre de la clase, pero no sería una técnica nativa del lenguaje.

### Acceso a las propiedades de un objeto

En Java se puede acceder a los atributos de un objeto de la siguiente forma:

{% highlight java %}
   for(Field field : objeto.getClass().getFields()){
      System.out.println( field.getName()+": "+ field.get(objeto));
   }
{% endhighlight %}

Y a los métodos:

{% highlight java %}
   for(Method method : objeto.getClass().getMethods()){
      System.out.println( method.getName()+": "+ method.toGenericString());
   }
{% endhighlight %}

En JavaScript se puede recorrer la lista de propiedades de un objeto (atributos y métodos) con el siguiente esquema:

{% highlight javascript %}
   for(var propiedad in objeto){
      console.log(propiedad+": "+objeto[propiedad]);
   }
{% endhighlight %}

Usando typeof se puede acceder sólo a los atributos, no a los métodos. 

{% highlight javascript %}
   for(var propiedad in objeto){
       var valorPropiedad = objeto[propiedad];
       if(typeof valorPropiedad !== 'function'){
          console.log(propiedad+": "+valorPropiedad);
       }
   }
{% endhighlight %}

Cuando se usa el patrón de clases con prototipos, se puede determinar si un método es de la clase hija o de cualquiera de las clases padre:

{% highlight javascript %}

var prototipo = Object.getPrototypeOf(objeto);

for(var propiedad in prototipo){
   if(typeof prototipo[propiedad] === 'function'){
      if(prototipo.hasOwnProperty(propiedad))
         //El método propiedad está en la clase hija
      } else {
         //El método propiedad está en alguna de las clases padre
      }
   }
}
{% endhighlight %}

Usando el patrón de clases con prototipos no se puede determinar si los atributos son de la clase hija o de la clase padre porque todos los atributos son propiedades del objeto.

Cuando se usa el patrón de clases con módulos no se puede determinar si los atributos o métodos están en la clase hija o en alguna de las clases padre porque todos los atributos y métodos son propiedades del objeto.

## Depuración

La depuración o ejecución paso a paso es una técnica muy útil en el desarrollo de programas. Sobre todo se utiliza para comprender el funcionamiento de un programa que se comporta de forma errónea. Aunque las técnicas de desarrollo _Test Driven Development_ han reducido la necesidad de utilizar la depuración, todavía sigue siendo una herramienta muy útil en manos del desarrollador. 

A la hora de elegir una técnica de implementación de clases en JavaScript es importante tener en cuenta el impacto que tiene la técnica elegida en el depurador. Cuando se implementan las clases como prototipos, los atributos de los objetos son propiedades del objeto y se pueden visualizar en el depurador. En cambio, cuando se usa la técnica de clases con módulos, como los atributos son variables en la closure de los métodos, esos atributos no se muestran en el depurador a no ser que estemos parados en un método que hace uso de esas variables. 

# Conclusión ¿Qué patrón usar?

Después de este repaso por la orientación a objetos en JavaScript tenemos que elegir qué patron usar de los tres disponibles:

* Clases con prototipos
* Clases con prototipos con librerías
* Clases con módulos

Aunque el uso de las librerías puede simplificar el código, algunos desarrolladres experimentados en JavaScript me dicen que actualmente (principios del 2014) no es una buena práctica en JavaScript definir jerarquías de clases usando estas librerías. Pero no tengo claro el motivo. No sé si están en contra de las librerías o del uso de los prototipos.

El autor de [JavaScript: The Good Parts][GoodParts] dice en [un post][HerenciaClasica] que intentar simular las jerarquías de herencia clásicas en JavaScript fue un error para él porque JavaScript tiene otros mecanismos de reutilización de código. Parece que está en contra de los artificios de las librerías por implementar el concepto de `super`, pero no entiendo muy bien su argumentación. No sé si está en contra de las librerías o del uso de los prototipos.

En esta respuesta a la pregunta [How to properly create a custom object in javascript][SO1] en StackOverlow su autor dice que no hay consenso sobre cual es mejor.

> Which way is “proper”? Both. Which is “best”? That depends on your situation. FWIW I tend towards prototyping for real JavaScript inheritance when I'm doing strongly OO stuff, and closures for simple throwaway page effects.

> But both ways are quite counter-intuitive to most programmers. Both have many potential messy variations. You will meet both (as well as many in-between and generally broken schemes) if you use other people's code/libraries. There is no one generally-accepted answer. Welcome to the wonderful world of JavaScript objects.

Además, hay que tener en cuenta las ventajas e inconvenientes de cada patrón. Hagamos un resumen de cada uno de ellos:

### Clases con prototipos

  * **Ventajas:** Es la forma nativa de implementar clases en JavaScript. Tiene mejor soporte de las herramientas de reflexión y depuración del lenguaje. Además, habrá más desarrolladores que comprendan el código, por tanto será más fácil compartir el código, corregir errores, etc. También es posible que esté más optimizado en los motores de JavaScript.
  * **Inconvenientes:** La sintáxis es verbosa y propensa a errors. No hay encapsulación en atributos ni métodos.

### Clases con prototipos con librerías

  * **Ventajas:** El código es más limpio. Es más fácil de entender por desarrolladores que tengan experiencia en prácticamente cualquier lenguaje de programacíón del planeta menos JavaScript, es decir, aquellos que tienen programación orientada a objetos con clases, no con prototipos. Es un azucar sintáctico para crear clases con prototipos, así que todas las ventajas de los prototipos también se tienen aquí. Incluso algunas librerías tiene su propia librería de reflexión.
  * **Desventajas:** Parece ser que usar estas librerías es _old school_ y no mola. No sé muy bien el motivo todavía. Depender de una librería con muchas funcionalidades sólo por la parte de creación de clases puede ser demasiado costoso, aunque hay librerías que se dedican exclusivamente a esto y son muy pequeñas. Como hay tropecientas librerías, hay una alta probabilidad de que la que tu elijas sólo la conozcas tu, obligando a los desarrolladores que quieran colaborar contigo a aprender una nueva librería por cada proyecto. 

### Clases con módulos

  * **Ventajas:** Tenemos bastante más encapsulación que con el patrón de prototipos. Todavía cualquiera puede cambiar los métodos de un objeto (consiguiendo el mismo efecto que modificando el valor de atributos privados), pero es más complicado de hacer por equivocación. También estamos menos expuestos al problema de que se olvide usar `new` para crear un objeto y a que se olvide hacer el `bind` cuando usamos los métodos como funciones independientes. 
  * **Inconvenientes:** No tenemos soporte de reflexión con las librerías del lenguaje. Puede haber un impacto en el consumo de memoria importante porque todos los objetos tienen todos los métodos. Los desarrolladores del lenguaje Ceylon (que compila a JavaScript) indican que [las clases con módulos pueden llegar a ser hasta 100 veces más lentas que las clases como prototipos][CeylonJS] en la máquina virtual V8. Y por último, el soporte del depurador es bastante más limitado con este patrón.

[CeylonJS]: http://ceylon-lang.org/blog/2012/01/02/prototypes-ceylon-js/

Entonces, ¿Qué hago? ¿Qué patron utilizo? La verdad es que no lo tengo claro.

¿Me puedes decir que opción usas tu y por qué lo haces en los comentarios? Seguro que me ayudas a elegir y a muchos que tienen las mismas dudas que yo.