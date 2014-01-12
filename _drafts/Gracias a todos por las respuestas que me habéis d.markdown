Gracias a todos por las respuestas que me habéis dado. Me están ayudando a entender la verdadera naturaleza de JavaScript.

Las conclusiones rápidas que obtengo son:
* JavaScript es funcional y orientado a objetos. Pero pesa más el paradigma funcional.
* El paradigma orientado a objetos se puede implementar con clases y objetos (como en CoffeeScript, Java, Ruby...) o sólo con objetos (prototipos).
* En JavaScript (un lenguaje funcional y con orientación a objetos basada en prototipos) la herencia no juega un papel tan importante como en los lenguajes basados en clases. Aunque últimamente también se considera que la herencia puede ser un antipatrón (Java Effective Programming: Item 16) incluso en los lenguajes con clases.

Supongo que mi desconcierto está motivado por varias cosas:
* Programar durante tanto tiempo con un único lenguaje tan "riguroso y limitado" como Java te amuebla la cabeza de una determinada forma y es difícil cambiar el chip.
* La evolución del lenguaje, librerías, frameworks y motores no ayuda nada a cambiar de chip porque las fuentes de información son muy confusas.
* He tenido mala suerte con los libros que he leído, porque esto no me lo han contado así en ninguno ;)

Libros que leer:

https://leanpub.com/javascript-allonge
JavaScript: The Definitive Guide by David Flanagan
Eloquent JavaScript by Marijn Haverbeke
JavaScript Patterns by Stoyan Stefanov
Writing Maintainable JavaScript by Nicholas Zakas
JavaScript: The Good Parts by Douglas Crockford

Libros leidos:

Patrones de diseño JS: 

Para continuar mi aprendizaje del lenguaje JavaScript, antes que aprender las bibliotecas más comunes (DOM, CommonJS, underscore, jquery...) he preferido aprender primero los patrones de diseño en JavaScript. Todavía no tengo claro cómo usar la orientación a objetos basada en prototipos y el paradigma funcional para estructurar una aplicación completa. Espero que conociendo los patrones de diseño JavaScript pueda entender mejor cómo hacerlo.

Siguiendo las recomendaciones de mis maestros, me he puesto a leer el libro [Essential JavaScript Design Patterns][DessignPatterns]. 

[DessignPatterns]: http://www.addyosmani.com/resources/essentialjsdesignpatterns/book/

## Patrón módulo

En un lenguaje orientado a objetos clases el programa se estructura con clases. Si queremos tener una serie de elementos de información y operaciones para trabajar con ellos, creamos una clase con esos elementos como atributos y las operaciones como métodos y sólo instanciamos un único objeto de esa clase. En programación estructurada, estaríamos hablando de un módulo, pero en Programación Orientada a Objetos con clases, se trata de una clase, como cualquier otra.

Para que exista una única instancia de una clase, basta con no crear más de un único objeto de la clase. Algunas veces es necesario que desde cualquier parte del programa se pueda acceder a esa única instancia. En ese caso se podrá usar el patrón singleton (creando un método estático en la clase que permita recuperar la única instancia, guardada en un atributo estático ). Otras veces se usará la inyección de dependencias, dejando que una entidad superior inyecte ese único objeto. 

JavaScript tiene dos características que hacen que esta solución en Java no se aplique directamente en él. Por un lado no tiene clases, sólo objetos. Por otro lado, existen un objeto global al que se le pueden añadir atributos que estarán disponibles desde el resto del programa. Estas características hacen que un módulo se implemente de forma completamente diferente a Java. 

Un módulo en JavaScript es un objeto asociado al objeto global como atributo y creado dentro de una función. Además, para tener cierto grado de encapsulación, la información gestionada por el módulo se implementa como variables locales a la función accesibles desde los métodos del objeto que definen el módulo. Además, como un módulo sólo se instancia una vez, justo después de definir la función es invocada. Lo que se llama "immediately-invoked functional expression". 

Un ejemplo de módulo:

// Global module
var myModule = (function () {
 
  // Module object 
  var module = {},
    privateVariable = "Hello World";
 
  function privateMethod() {
    // ...
  }
 
  module.publicProperty = "Foobar";
  module.publicMethod = function () {
    console.log( privateVariable );
  };
 
  return module;
 
})();

No obstante, también se puede implementar el patrón singleton como es conocido en POO cuando existen varias instancias de la clase (o de clases hijas) que se devuelven en función de un parámetro o cuando se requieran ciertas tareas de inicialización que sólo tenga sentido hacer cuando se accede realmente al objeto.












Cómo definir clases en JavaScript: http://www.phpied.com/3-ways-to-define-a-javascript-class/

IDE en el navegador: http://jsbin.com/UMEJaXu/1/edit
