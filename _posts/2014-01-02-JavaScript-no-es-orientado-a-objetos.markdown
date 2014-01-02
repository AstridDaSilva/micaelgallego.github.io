---
layout: post
title: JavaScript no es Orientado a Objetos (VTF4)
category: front-end
tags: javascript poo prototipos dinámico java
year: 2014
month: 1
day: 1
published: true
summary: Después de intentar comprender la orientación a objetos de JavaScript desde la visión de la orientación a objetos de Java, C++, Python o Ruby comprendo que JavaScript tiene su propia filosofía. 
image: viaje-front-end/JavaScript-logo.png
---

Esta es la cuarta entrega de una serie de posts en los que cuento mi viaje por las tecnologías de front-end, esas que permiten implementar aplicaciones web interactivas. Todo ello desde el punto de vista de un programador Java con más de 10 años de experiencia. Si te interesa puedes echar un vistazo a las partes anteriores:

* Parte 1: [Viaje por las tecnologias de front end][Parte 1]
* Parte 2: [Primer contacto con JavaScript][Parte 2], 
* Parte 3: [Orientacion a Objetos en JavaScript comparado con Java][Parte 3]

[Parte 1]: /blog/Viaje-por-las-tecnologias-de-front-end
[Parte 2]: /blog/Viaje-por-las-tecnologias-de-front-end2
[Parte 3]: /blog/Orientacion-a-Objetos-en-JavaScript-comparado-con-Java

# Las características familiares de JavaScript para un desarrollador Java

Después de haberme leído varios libros sobre JavaScript, entendía más o menos bien todos los conceptos del lenguaje:

* **Es un lenguaje dinámico**: Entre otras muchas cosas, eso significa que no tiene compilador. Un intérprete o _engine_ es el encargado de ejecutar el código fuente. 
* **Es un lenguaje con tipado dinámico:** Eso quiere decir que las variables no tienen tipo. Una misma variable puede tener valores de diferentes tipos a lo largo de su vida.
* **Tiene tres tipos básicos:** Números, booleanos y cadenas de caracteres (String). Esto tiene sentido en un lenguaje que no está preocupado por la eficiencia y sí en ser muy sencillo de usar. Al fin y al cabo, la separación entre números real y entero y entre char y string son sobre todo cuestiones de eficiencia. 
* **Tiene un sistema de tipos unificado:** De forma que un entero y un string son de la misma naturaleza. 
* **Tiene sentencias de control de flujo "normales":** Es decir, que tiene if, while, for, switch etc.. con la sintáxis y semática a la que estamos acostumbrados los programadores Java. Incluso he visto que tiene excepciones, como en Java. 
* **Tiene arrays y se gestionan "por referencia":** Es decir, un array es conceptualmente muy similar a como es en Java. Cuando se pasa como parámetro, se pasa la referencia (no hay copia), de forma que los cambios en el array son visibles por todos aquellos que tengan la referencia al array. 
* **Existe un recolector de basura:** Perfecto, un comportamiento similar a Java, Python, Ruby, Scala, C#...

Hasta aquí todo razonable. Estoy en un sitio conocido ;). Es cierto que no tengo mucha experiencia con lenguajes con tipado dinámico, pero siempre he entendido que si no pones el tipo a una variable, tendrás que tener mucho más cuidado de no equivocarte en el valor que asignas porque el compilador no te avisará si te equivocas. Es decir, salvo ese detalle, todo es conceptualmente similar.

# Programación funcional en JavaScript

Una de las características importantes de JavaScript es que es un lenguaje funcional. Es funcional porque trata las funciones como ciudadanos de primera clase en el lenguaje. Se pueden declarar, se pueden invocar, se pueden guardar en variables y se pueden pasar como parámetro a otras funciones. No es funcional puro, porque puedes declarar variables y cambiar su valor y las funciones se pueden implementar sin transparencia referencial. Es decir, que pueden tener efectos colaterales y varias llamadas a la misma función pueden devolver resultados diferentes.

Java todavía no es un lenguaje funcional. Pero las clases anónimas han permitido programar conceptualmente de forma funcional. Librerías como [Guava][] han favorecido la programación funcional con estructuras de datos. Además, como seguro que ya sabes, en Java 8 las funciones cobrarán mucha más importancia en el lenguaje a través de las [expresiones lambda][]. 

Por todo esto, la programación funcional de JavaScript es bastante natural y conocida para un desarrollador de Java como yo.

Sólo hay un "pequeño detalle" que diferencia las funciones de Java (sean clases anónimas o expresiones lambda) de las funciones en JavaScript. En JavaScript las funciones tienen acceso a las variables que se encuentran en el ámbito en el que se declara la función. Y si esa variable cambia de valor y se ejecuta la función, se leerá el nuevo valor. El conjunto de variables a las que tiene acceso la función se le conoce como _closure_ o clousura. En Java esto no es posible, si se accede a una varible del ámbito, esa variable no puede cambiar de valor, porque en realidad se hace referencia al valor, no a la variable. 

Que JavaScript soporte clousuras es esencial en este lenguaje. La forma de programar en JavaScript está profundamente motivada por esta característica. Al principio puede parecer un detalle más, pero como veremos más adelante, es muy importante.

[expresiones lambda]: http://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html
[Guava]: http://code.google.com/p/guava-libraries/wiki/FunctionalExplained

# La orientación a objetos "clásica" en JavaScript

Todas las características de JavaScript que he mencionado hasta ahora son bastante conocidas para un desarrollador Java. Es decir, un programador Java se siente bastante cómodo usando esas características porque las usa habitualmente en el desarrollo de sus programas. Siempre hay detalles que tener en cuenta, pero conceptualmente todo es bastante similar. 

## Tres formas de implementar la orientación a objetos ¿Cual es la buena?

El problema aparece cuando llegamos a la programación orientada a objetos. Según aprendía el lenguaje leí que JavaScript es un lenguaje orientado a objetos. Entonces pensé: perfecto, como en Java, Python, Ruby... Ahora sólo tenía que conocer la sintáxis. Estuve leyendo que JavaScript está basado en prototipos y no en clases. Pensé que era sólo uno de los detalles de JavaScript, pero que conceptualmente era equivalente a Java. Pero en ese momento llegaron los problemas. 

Según leía diferentes libros y páginas de Internet me enteré de que había tres formas diferentes de implementar la orientación a objetos en JavaScript. Cada una de ellas con diferentes ventajas e inconvenientes. No entendía nada, ¿por qué hay tantas formas diferentes de implementar lo mismo? ¿Por qué no se usa una de las formas? Como no lo tenía nada claro, me puse a buscar más información por Internet, a leer más libros... pero las dudas crecían en vez de despejarse. Llegados a este punto decidí que la mejor forma de resolver mis dudas era preguntar a los desarrolladores experimentados en JavaScript que conocía. Hice un [estudio exahustivo de las tres formas diferentes de implementar la orientación a objetos en JavaScript][Parte 2] y recopilé las ventajas e inconvenientes de cada uno de ellos. Ese estudio serviría para poder preguntar, ¿cómo se implementa la orientación a objetos en JavaScript?

Con este estudio pregunté por twitter:

<blockquote class="twitter-tweet" lang="es"><p>Comparación de la Orientación a Objetos en Java y JavaScript. Después de leer 4 libros no me aclaro. Me ayudas? <a href="http://t.co/5mmgyJbquI">http://t.co/5mmgyJbquI</a></p>&mdash; Micael Gallego (@micael_gallego) <a href="https://twitter.com/micael_gallego/statuses/417668476438724608">diciembre 30, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Y también pregunté en el [grupo Meetup de MadridJS](http://www.meetup.com/madridjs/messages/62930352).

Gracias a los camaradas del métal que me respondieron en la lista del meetup, a los comentarios del blog y a lo que me fueron comentando algunos amigos empecé a ver la luz.

## No hay una forma buena, JavaScript no es orientado a objetos

Al principio las respuestas eran más confusas todavía, porque no contestaban a la pregunta. Yo pregunté cual es la mejor forma de implementar la orientación a objetos en JavaScript, pero las respuestas venían a decir que en JavaScript la orientación a objetos no es igual que en otros lenguajes y por tanto intentar aplicar los mismos conceptos que en los otros lenguajes no es la forma habitual de programar en JavaScript. Como diría alguien conocido por todos, me quedé con el culo torcío ;)

# La orientación a objetos "especial" de JavaScript

Cuando uno lleva tanto tiempo programando con Java, tiene experiencia con patrones de diseño orientados a objetos y conoce algo de C++, Ruby y Python cree que conoce bien qué es la programación orientada a objetos. Piensa que sabe como usar este paradigma de programación para implementar programas modulares, comprensibles, con partes reutilizables y que son fácilmente ampliables y mantenibles.

Cuando empiezas a estudiar JavaScript crees que lo único que tienes que hacer es aprender la sintáxis para implementar las clases y esos pequeños detalles que diferencian a JavaScript de otros lenguajes que conoces. Además, como he comentado antes, yo no he tenido experiencia con lenguajes con tipado dinámico, pero pensaba que la diferencia fundamental con los lenguajes con tipado estático era que en las variables no se indica el tipo y cuando se ejecuta el programa se "verifica" si el uso de la variable es el correcto para el valor que tiene. 

Pero estaba completamente equivocado. En JavaScript, la orientación a objetos es conceptualmente muy diferente a la orientación a objetos de Java y otros lenguajes. Por otro lado, en JavaScript los objetos son dinámicos, es decir, pueden cambiar estructuralmente durante la ejecución del programa. Al principio parece que estos dos detalles no son importantes y que conceptualmente Java y JavaScript son bastante parecidos. Pero luego te das cuenta de que esas pequeñas diferencias superficiales afectan de forma importante a la forma de programar con un lenguaje u otro.

## Programación orientada a objetos en Java, C#, C++, Python, Ruby...

Antes de explicar cómo se implementa la orientación a objetos en JavaScript, vamos a repasar qué entendemos por orientación a objetos en los lenguajes de programación más conocidos como Java, C#, C++, Python, Ruby, etc. En estos lenguajes se utilizan las clases para definir los métodos y los atributos que tendrán los objetos de esas clases. Eso implica que todo objeto es una instancia de una clase, y esa clase define los métodos y los atributos del objeto. Si nos olvidamos de los atributos estáticos, cada objeto de una clase posiblemente tendrá valores en sus atributos diferentes a los valores de otros objetos de la misma clase. Por otro lado, los métodos serán exactamente iguales para los objetos de una misma clase. 

En los lenguajes estáticos (Java, C++, C#) no se pueden modificar las clases en tiempo de ejecución. Es decir, no se pueden añadir o quitar atributos o métodos de los objetos de una clase durante la ejecución del programa. Ya sé que técnicamente es posible y en Java se hace en diversas situaciones especiales, pero no es una técnica que se use de forma natural en el propio lenguaje para escribir programas. En los lenguajes dinámicos como Python, Ruby, Smalltalk si se puede modificar una clase en tiempo de ejecución, aunque no sé si se utiliza habitualmente para programar o es una funcionalidad destinada a "ocasiones especiales".

## Programación orientada a objetos en JavaScript

En JavaScript no existen las clases. En JavaScript sólo existen objetos. Pero estos objetos son muy flexibles y se les puede añadir atributos y métodos en el momento de la creación, justo después de haberlos creado o en cualquier momento a lo largo de la ejecución del programa. Esta es la clave de la programación orientada o objetos en JavaScript. Por ejemplo, si queremos crear un objeto que representa un empleado de una empresa podemos hacer lo siguiente:

{% highlight javascript %}
var empleado = {
   nombre: "Pepe",
   salario: 700,
   toString: function(){
      return "Nombre:"+this.nombre+", Salario:"+this.salario;
   }
};
{% endhighlight %}

Y si queremos invocar un método o acceder a un atributo usaríamos la sintaxis a la que estamos acostumbrados en Java u otros lenguajes, la notación punto:

{% highlight javascript %}
var texto = empleado.toString();   //Devuelve 'Nombre:Pepe, Salario:700'
var salario = empleado.salario;    //Devuelve 700
{% endhighlight %}

En cualquier momento posterior le podemos añadir un nuevo método o atributo al objeto. Por ejemplo, podemos asignar un teléfono al empleado y un método para obtener la categoría:

{% highlight javascript %}
empleado.telefono = "663232539";
empleado.getCategoria = function(){
   return salario > 800 ? "Superior":"Normal";
}
{% endhighlight %}

Al principio te puede parecer que esta forma de trabajar con los objetos es muy rara, no es intuitiva. Pero eso es porque estás tan acostumbrado a trabajar con clases, como yo, que no entiendes muy bien qué sentido tiene hacerlo así. Pero de momento no vamos a entrar a valorar si tiene o no tiene sentido, si es mejor o es peor tener tanta flexibilidad. De momento vamos a comprender como funciona la orientación a objetos en JavaScript y al final de la entrada haremos la valoración comparando los dos modelos. 

### Múltiples objetos con la misma estructura

Cuando implementamos un programa es habitual que tengamos varios objetos estructuralmente iguales, es decir, que tengan los mismos atributos y los mismos métodos. Por eso usamos las clases en Java, para definir el molde con el que se crearán los objetos que sean instancias de esa clase. En JavaScript, si queremos que varios objetos sean estructuralmente iguales podemos encapsular el código de creación del objeto en una función. Por ejemplo, de la siguiente forma:

{% highlight javascript %}
function newEmpleado(nombre, salario){
   var empleado = {
      nombre: nombre,
      salario: salario,
      toString: function(){
        return "Nombre:"+this.nombre+", Salario:"+this.salario;
      } 
   };
   return empleado;
}
{% endhighlight %}

Y así podremos llamar a esa función para crear los objetos:

{% highlight javascript %}
var empleado = newEmpleado("Pepe",700);
var texto = empleado.toString();   //Devuelve 'Nombre:Pepe, Salario:700'
var salario = empleado.salario;    //Devuelve 700
{% endhighlight %}

Como ves, no hay clases por ningún sitio. Si quieres pensar que la función 'newEmpleado' es en realidad una clase, puedes hacerlo, pero estarías cometiendo el mismo error que si llamaras registo a una clase de Java. No es una clase porque no es un molde de sus objetos.

### Prototipos

Si nos fijamos en la creación del empleado, nos damos cuenta que los atributos `nombre` y `salario` pueden tener valores diferentes para cada objeto. Pero en realidad, el método `toString` es siempre el mismo en cada objeto. Por otro lado, si quisiéramos añadir el método `getCategoría` a todos los objetos empleado que hemos creado, tendríamos que ir uno por uno y añadir el método. En estos casos sería deseable que todo aquello que compartan todos los objetos empleado estuviera en un lugar común que se gestione de forma unificada para todos ellos.

En JavaScript, cualquier objeto puede estar asociado a un **objeto prototipo**. El objeto prototipo es un objeto normal, como cualquier otro. Cuando un objeto está asociado a un prototipo se comporta de la siguiente forma:

* Cuando se accede a un atributo en un objeto y no existe en dicho objeto, se busca en su prototipo y se devuelve su valor.
* Cuando se escribe en un atributo y no existe el atributo en ese objeto, se crea el atributo en el objeto. Por tanto el valor se cambia en el objeto, no en el prototipo.
* Cuando se intenta ejecutar un método en un objeto y no existe en dicho objeto, se busca en su prototipo y se ejecuta.
* A un objeto se le pueden añadir y quitar atributos y métodos en tiempo de ejecución, pero [no puede cambiar de prototipo][NoCambioPrototipo].

[NoCambioPrototipo]: http://stackoverflow.com/questions/7015693/how-to-set-the-prototype-of-a-javascript-object-that-has-already-been-instantiat

Por ejemplo, si queremos que todos los empleados estén asociados a un mismo objeto prototipo que contenga los métodos (que son iguales para todos los empleados), podriamos usar un código como el siguiente: 

{% highlight javascript %}
var prototipoEmpleado = {
   toString: function(){
     return "Nombre:"+this.nombre+", Salario:"+this.salario;
   }
};

function newEmpleado(nombre, salario){
   var empleado = Object.create(prototipoEmpleado);
   empleado.nombre = nombre;
   empleado.salario = salario;
   return empleado;
}
{% endhighlight %}

El uso del objeto no cambia. Se podría decir que el prototipo es un detalle de implementación del objeto empleado que no afecta a los usuarios del objeto.

Usando un prototipo, si queremos añadir un método a todos los objetos empleado, bastaría con que añadamos el método al objeto que hace de prototipo:

{% highlight javascript %}
prototipoEmpleado.getCategoria = function(){
   return salario > 800 ? "Superior":"Normal";
}
{% endhighlight %}

Por supuesto, el objeto `prototipoEmpleado` puede tener otro prototipo y así, sucesivamente. Es decir, se puede formar una **cadena de prototipos**. 

Si se usan prototipos se tiene la ventaja de tener un menor consumo de memoria porque los métodos compartidos por todos los objetos estarán en el prototipo. Pero también hay un inconveniente, y es que hay una pequeña sobrecarga al ejecutar un método porque hay que buscar el método en la cadena de prototipos. 

Es decir, no siempre se usan los prototipos en JavaScript. Por ejemplo, en los siguientes casos no se usan:

* Cuando sólo se necesita un objeto con unos determinados atributos y métodos.
* Cuando el código es más sencillo y compacto si no se crea la función que permite crear objetos, aunque haya varios objetos con los mismos atributos y métodos.
* Cuando la reducción en el tiempo de ejecución de los métodos es preferible al posible impacto en memoria que se tendría al tener los métodos en el prototipo.

## Clases frente a prototipos

Hemos visto como la programación orientada a objetos de Java, Ruby, Python, C++, C#... es muy diferente a la programación orientada a objetos de JavaScript. Eso es porque existen dos formas de implementar la orientación a objetos en un lenguaje de programación: **basada en clases** y **basada en prototipos**. Además de JavaScript existen más lenguajes que implementan la programación basada en prototipos, pero se usan principalmente en el ámbito académico.

Si estás interesado en los detalles más teóricos de un modelo frente a otro, existe mucha documentación por la red sobre el modelo de orientación a objetos basado en prototipos, sobre todo en comparación con el modelo basado en clases:

* [Documentación oficial de Mozilla](https://developer.mozilla.org/es/docs/Gu%C3%ADa_JavaScript_1.5/Lenguajes_basados_en_clases_frente_a_basados_en_prototipos)
* [Artículo "Programación Orientada a Objetos: Clases versus Prototipos" en la revista Novática](http://trevinca.ei.uvigo.es/~pcuesta/publicaciones/prototipos.pdf)
* [Programación basada en prototipos en la wikipedia](http://en.wikipedia.org/wiki/Prototype-based_programming)

# Funciones constructor, prototipos y reflexión

Como JavaScript se diseñó en un momento en el que el lenguaje Java era muy popular, sus creadores intentaron que JavaScript se pareciera a Java lo más posible. Pero en vez de elegir el modelo de orientación a objetos similar a Java (como han hecho otros lenguajes dinámicos), eligieron que la sintaxis fuera parecida aunque el modelo de programación fuera diferente. Uno de los autores más reputados en el mundo de JavaScript, Douglas-Crockford, autor del libro [JavaScript: The Good Parts][GoodParts], considera que intentar imitar la sintaxis de Java pero con otro modelo ha sido muy perjudicial para el lenguaje. Porque los desarrolladores de Java ven una sintaxis familiar y se esperan un comportamiento similar, pero los detalles de funcionamiento son muy diferentes. 

## Función constructor y prototipo

Para intentar emular a Java, si en JavaScript se llama a una función antecediendo el operador `new`, entonces se crea de forma automática un objeto, ese objeto se puede utilizar desde el cuerpo de la función usando la variable implícita `this` y además eso objeto se devuelve de forma automática al terminar de ejecutarse la función. Es decir, esta función que habíamos implementado antes:

{% highlight javascript %}
function newEmpleado(nombre, salario){
   var empleado = Object.create(prototipoEmpleado);
   empleado.nombre = nombre;
   empleado.salario = salario;
   return empleado;
}
{% endhighlight %}

Y que se utliza usando la sintáxis:

{% highlight javascript %}
var empleado = newEmpleado("Pepe",700);
{% endhighlight %}

Se puede implementar de la siguiente forma:

{% highlight javascript %}
function Empleado(nombre, salario){
   this.nombre = nombre;
   this.salario = salario;
}
{% endhighlight %}

Si se llama usando la sintáxis:

{% highlight javascript %}
var empleado = new Empleado("Pepe",700);
{% endhighlight %}

Los objetos creados usando la función `Empleado` tendrán como prototipo el objeto `Empleado.prototype`. Es decir, si queremos que el prototipo de los objetos empleado tenga el método `toString`, tenemos que usar el siguiente código:

{% highlight javascript %}
Empleado.protoype.toString = function(){
   return "Nombre:"+this.nombre+", Salario:"+this.salario;
};
{% endhighlight %}

Como se puede ver, la función `Empleado` tiene atributos, en concreto, el atributo `prototype`. En JavaScript las funciones son objetos y como tales pueden tener atributos. 

Cuando una función se ejecuta usando el operador `new` se dice que esa función es un **constructor**. Hay que tener mucho cuidado cuando se usa un constructor, porque si se ejecuta sin el operador `new` no se genera ningún error en tiempo de ejecución pero pueden ocurrir cosas inesperadas y no deseadas (otro fallo de diseño del lenguaje). 

Como se puede ver, la sintáxis recuerda a Java, pero en realidad no hay clases, sólo hay funciones "especiales" que tienen azúcar sintáctico para crear objetos. Además, aunque se pueden usar las funciones constructor, no siempre se usan para crear objetos. En muchas ocasiones los objetos se crear con la sintaxis literal que se ha visto antes.

[GoodParts]: http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742

## Reflexión y duck typing

En el desarrollo de un programa, en algunas ocasiones es necesario programar de forma reflexiva. En Java existen diversas formas de reflexión. La más sencilla es preguntar por la clase de un objeto, para hacer casting e invocar alguno de sus métodos. Pero también podemos preguntar por los métodos que tiene un determinado objeto (por pertenecer a una determinada clase). En JavaScript la reflexión se entiende de forma diferente.

### Conocer el prototipo de un objeto

El lenguaje JavaScript dispone del método [getPrototypeOf][] para obtener el prototipo de un objeto:

{% highlight javascript %}
var empleado = new Empleado("Juan",444);
if(Object.getPrototypeOf(empleado) === Empleado.prototype){
   //...	
}
{% endhighlight %}

Como puede haber una cadena de prototipos, se puede usar el método [isPrototypeOf][] para saber si un prototipo está en la cadena de prototipos de un objeto:

{% highlight javascript %}
var empleado = new Empleado("Juan",444);
if(Empleado.prototype.isPrototypeOf(empleado)){
   //...	
}
{% endhighlight %}

Con el objetivo de parecerse a Java, en JavaScript existe el operador [instanceof][]. Este operador sirve para saber si un determinado prototipo está en la cadena de prototipos de un objeto. Pero en vez de pasar como segundo operando el propio prototipo, se pasa la función constructor. Es decir, el código equivalente al anterior sería algo así:

{% highlight javascript %}
var empleado = new Empleado("Juan",444);
if(empleado instanceof Empleado){
   //El objeto empleado tiene como prototipo al objeto Empleado.prototype.
}
{% endhighlight %}

Pero hay que tener en cuenta de que en JavaScript no sirve de mucho preguntar por el objeto prototipo de otro objeto. Hay veces que se utilizan objetos que no tienen prototipo, porque todos sus atributos y métodos son propiedades del propio objeto. Y esto es relativamente normal en JavaScript. 

En Java es mucho más importante preguntar por la clase de un objeto, porque es la única forma que tenemos de conocer los métodos de ese objeto y haciendo un casting los podremos invocar. Pero en JavaScript, para poder invocar un método, basta con que ese método exista en el objeto. El método puede estar en el propio objeto o a través de su cadena de prototipos, pero eso es completamente indiferente.

[instanceof]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof
[isPrototypeOf]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/isPrototypeOf
[getPrototypeOf]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf 

### Duck typing

Como en JavaScript no existen las clases, no tiene sentido preguntar por el tipo de un objeto, porque todos los objetos son de tipo `Object`. Podemos considerar que un objeto prototipo hace de "tipo", pero es sólo una interpretación que hacemos del funcionamiento de los prototipos cuando venimos de un lenguaje basado en clases. Pero si hubiésemos aprendido la orientación a objetos con JavaScript, el concepto de clase nos hubiese sonado muy poco intuitivo. El propio lenguaje ayuda en esta confusión, porque el operador `new`, las funciones constructor y el operador `instanceof` hacen pensar en los prototipos como una especie de clases. En perspectiva, muchos autores consideran que estos operadores han podido ser un error de diseño del lenguaje porque provoca confusión.

Para invocar un método en un objeto en JavaScript basta con invocar el método en el objeto. No hay que preguntar por el tipo, no hay que hacer casting, simplemente hay que ejecutar el método. Si el método existe, es que el objeto es del "tipo" esperado. Si no existe, entonces el objeto no es del tipo esperado. En realidad en JavaScript no existen clases, así que no tiene mucho sentido afirmar que un objeto es "del tipo esperado". En Python, un lenguaje con clases, se utiliza esta técnica de invocar un método en un objeto sin preocuparse por la clase del objeto. Si el método existe, perfecto, si no, se produce un error. A esta técnica se la conoce como [duck typing][]. El nombre se debe a un ejemplo que se usaba para explicar este mecanismo de programación: 

> "Cuando veo un ave que camina como un pato, nada como un pato y suena como un pato, a esa ave yo la llamo un pato."

Si el método que queremos invocar no éstá disponible, se producirá un error en tiempo de ejecución. Dependiendo de cómo estemos programando nuestro programa, que el objeto no tenga el método puede suponer un error de programación o una situación aceptada. Si es un error de programación, debería corregirse. Si es una situación esperada, se podría comprobar la existencia del método antes de invocarlo o bien se podría capturar la excepción.

[duck typing]: http://es.wikipedia.org/wiki/Duck_typing

# Simulación de clases en JavaScript

JavaScript no tiene clases, tiene objetos dinámicos y prototipos. Esto implica que un programa en JavaScript es muy diferente a un programa en Java. 

En Java, un programa es un conjunto de clases que se relacionan entre sí (composición, asociación, uso y herencia). Durante la ejecución, un programa es un conjunto de objetos de esas clases que colaboran entre sí mediante las reglas marcadas por sus clases.

En JavaScript no hay clases, sólo hay objetos y funciones. Por tanto, la estructura del código es muy diferente. En una sección al final podremos ver cómo se estructura un programa en JavaScript, pero de momento quiero dejar claro que es de otra forma a como se hace en Java. 

Un desarrollador Java puede intentar "emular" todo lo que conoce de la programación orientada a objetos basada en clases de Java y aplicarlo en JavaScript. De hecho, hay muchos desarrolladores que lo han hecho de esta forma. Han creado artificios en JavaScript para que el modelo de programación sea como un modelo basado en clases. 

En concreto, existen tres formas comúnmente aceptadas de programar simulando clases en JavaScript:

* Clases con prototipos
* Clases con prototipos usando librerías
* Clases con módulos (basados en clousuras)

Si quieres saber más detalles de estas formas de programar, con sus ventajas e inconvenientes, puedes echar un vistazo al [estudio que hice comparando cada una de ellas][Parte 3].

Pero es muy importante saber que si decides estructurar tu programa con clases como lo haces en Java estarás haciendo las cosas de forma poco natural. Sobre todo si utilizas jerarquías de herencia entre clases. Los desarrolladores de JavaScript usan programación orientada a objetos porque manejan objetos dinámicos. En ciertos casos, se definen prototipos y funciones constructor, pero es más raro ver jerarquías de herencia de clases en programas JavaScript. Hace años era más habitual que los desarrollodores JavaScript intentaran estructurar un programa únicamente con clases, como en Java, pero actualmente se considera que no es una buena práctica, porque las características del lenguaje permiten programar de otra forma más directa, concisa y versátil.

Es como si un desarrollador de C programara en Java con clases sin atributos y con métodos estáticos (como módulos) y con clases con atributos públicos y sin métodos (como structs). Estaría implementando programación estructurada en Java. Lo mismo les ocurre a los programadores de C que usan [GObject][], la librería de objetos de la gente de GNOME. Han montado un sistema de objetos encima del lenguaje C. No está mal, cumple sus objetivos, pero es un artificio sobre el lenguaje. 

Otra cosa muy importante es que tu puedes programar con el artificio que tu quieras. Pero si quieres leer código de otros, tendrás que comprender su funcionamiento, y es bastante probable que ellos no usen el mismo artificio que tu, porque hay miles de formas diferentes de simular clases en JavaScript. Si vas a programar en equipo tendrás que acordar con tus compañeros una forma de programar, y es posible que no se utilice la forma que a ti más te gusta. Es decir, que sea como sea, tendrás que conocer en profundidad cómo funciona JavaScript y los idiomas aceptados en este lenguaje. 

[GObject]: http://es.wikipedia.org/wiki/GObject

# CoffeScript y sus clases

Hay muchos programadores que piensan que la sintáxis de JavaScript es muy verbosa y no es la más adecuada para un lenguaje dinámico. Estos programadores suelen utilizar otros lenguajes dinámicos como Ruby y Python y languajes funcionales como Haskell. 

Para sentirse más cómodos, estos desarrolladores han creado el lenguaje de programación **[CoffeScript][]**, un lenguaje que se traduce a JavaScript. Su regla de oro es que "Es sólo JavaScript" y se puede considerar como azucar sintáctico sobre JavaScript. En general mantiene los mismos conceptos que JavaScript. Es decir, no lo utliza como si fuera el [ensamblador de la web][], simplemente es una fina capa por encima. De hecho, algunos piensan que para usar CoffeeScript [primero tienes que saber JavaScript][], cosa que yo he experiementado en mis propias carnes. En otros contextos, no tendría sentido hacer un lenguaje como CoffeeScript, tendría más sentido hacer un lenguaje completamente nuevo, pero la web es un sitio muy especial ;).

[sintaxis para crear clases]: http://coffeescript.org/#classes
[CoffeScript]:http://coffeescript.org/ 
[ensamblador de la web]: http://www.hanselman.com/blog/JavaScriptIsWebAssemblyLanguageAndThatsOK.aspx
[primero tienes que saber JavaScript]: http://carlossanchezperez.wordpress.com/2013/06/16/antes-de-meterte-en-coffeescript-recomendable-haber-pasado-por-javascript-primera-parte/

Aparte de todo el azúcar sintáctico, una de las cosas que pretende mejorar CoffeeScript es la [sintaxis para crear clases][]. En CoffeeScript se pueden implementar clases apoyándose en los prototipos de JavaScript, pero con una sintaxis mucho más parecida a los lenguajes que realmente tienen clases. Puedes implementar clases con `class`, `extends` y `super`. 

Pero CoffeeScript no te fuerza a estructurar tu programa con clases, simplemente te facilita el uso de prototipos como si fueran clases con una sintáxis más concisa. Pero si prefieres trabajar directamente con prototipos, también te ofrece operadores para tratar directamente con ellos.

# Estructura de una aplicación JavaScript

La estructura de una aplicación depende de muchos factores. En Java se pueden tener diversos tipos de aplicaciones, por mencionar algunas:

* **Aplicación de escritorio con Swing**: En este caso lo más probable es que la aplicación sea una colección de clases relacionadas entre sí y una de ellas tendrá un método estático `main` que contendrá las sentencias que incian la ejecución de la aplicación. Posiblemente no haya ningún fichero de configuración.
* **Aplicación web con Spring**: Lo más probable es que, además de las clases que forman la aplicación, tengamos dos ficheros de configuración: `web.xml` y `application-context.xml`.

En JavaScript ocurre lo mismo, dependiendo del tipo de aplicación, la estructura será muy diferente. Pero sea como sea la estructura de la aplicación, hay que tener en cuenta que no hay clases. Por tanto, la aplicación estará estructurada con otros elementos de alto nivel.

Si consideramos la aplicación más básica en JavaScript que se ejecuta en el navegador posiblemente usará la librería [jQuery][] y [underscore.js][]. En el momento de escribir este post, estas librerías se consideran esenciales (al menos esa es la sensación que tengo). La aplicación tendrá la siguiente estructura:

[jQuery]: http://jquery.com/
[underscore.js]: http://underscorejs.org/

`index.html`

{% highlight html %}
<!DOCTYPE html>
<html>
   <head>
      <script src="http://code.jquery.com/jquery-1.7.2.js"></script>
      <script src="http://underscorejs.org/underscore.js"></script>
      <script src="app.js"></script>
   </head>
   <body>
      <div id="primenumbers">Prime numbers</div>
      <div id="theirsquares">Their squares</div>
   </body>
</html>
{% endhighlight %}

`app.js`

{% highlight javascript %}
$(function() {

    var primeNumbers = [2, 3, 5, 7, 11];
        
    var listIn = function(selector) {
        return function(num){
            $(selector).append('<p>' + num + '</p>');
        };
    };
        
    _.each(primeNumbers, listIn('#primenumbers'));

    var square = function(num) { return num * num; };
    _.each(_.map(primeNumbers, square), listIn('#theirsquares'));
        
});
{% endhighlight %}    

Si no tienes experiencia con JavaScript y con las librerías jQuery y underscore, este código te puede parecer un poco difícil de entender. A continuación se muestran algunas claves:

* Los símbolos `$` y `_` son identificadores que usan la librería jQuery y underscore para declarar sus utilidades. Se usan estos nombres tan cortos para que sean muy sencillos de usar en un programa.
* `$` es una función definida globalmente por jQuery. La expresión `$(selector).append(...)` es la invocación de una función que devuelve un objeto en el que se invoca el método `append`.
* `_` es un objeto definido globalmente por la librería underscore, por eso la expresión `_.each(...)` es la invocación de un método del objeto `_`.
* El código de la aplicación está en una función anónima que se pasa como parámetro a la función `$`. La función pasada como parámetro será invocada cuando el documento se haya cargado en el navegador, pero sin necesidad de que se hayan cargado todas las imágenes y recursos asociados.

Como se puede ver, la estructura de la aplicación no se parece nada a un conjunto de clases que colaboran entre sí. Por tanto, aunque utilices clases en tu aplicación, será sólo en ciertas partes de la misma, pero las clases no definirán la estructura como lo harían en un programa Java. 

# Conclusiones

Cuando empecé a aprender de JavaScript pensaba que era un lenguaje parecido a Java, salvo por ser de tipado dinámico en vez de tipado estático. Esta confusión quizás se debió a que llevo mucho tiempo programando con Java y en mis pinitos con Ruby y Python las cosas eran bastante naturales para mí porque todos los lenguajes se parecían bastante.

También he de decir que los libros que he leído no me han ayudado mucho. Quizás ha sido mi ceguera conceptual y lo que ahora entiendo estaba perfectamente especificado en los libros, pero me da la sensación de que algunos de los libros que he leído no respondían a las preguntas que yo me estaba haciendo o las respuestas que obtenía me llevaban a sacar conclusiones equivocadas.

En cualquier caso, ahora ya lo entiendo todo. La orientación a objetos que yo he practicado durante tanto tiempo no es la única que existe. Existen otros lenguajes que siendo orientados a objetos, no tienen clases, y eso lo cambia todo. Es posible que haya partes de un programa JavaScript que resulten familiares a un desarrollador acostumbrado a usar la orientación a objetos de clases en Java. Pero sin duda alguna, la estructura del programa JavaScript nada tiene que ver con la estructura de un programa Java.

Ya he entendido las características del lenguaje JavaScript, pero todavía no las puedo valorar. Hasta que no lleve un tiempo programando con JavaScript, no podré tener una opinión. Quizás me enamore de esa versatilidad y libertad prácticamente total que me ofrece el lenguaje, y cuando tenga que programar en Java me sienta encorsetado en una estructura rígida y llena de protocolo y ceremonia. O quizás me pase justo lo contrario, que esa libertad me haga muy difícil entender código JavaScript de otros desarrolladores o que yo mismo vaya mucho más lento programando por no tener claro cómo hacer esto o lo otro. 

Dentro de un tiempo os contaré mis impresiones ;). Si quieres, puedes compartir con nosotros tu experiencia en los comentarios. 

