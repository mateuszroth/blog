---
title: JavaScript static classes, methods & properties
tags:
  - JavaScript
categories:
  - [JavaScript, Basics]
date: 2020-07-17 21:25:00
---
# Static methods

In other words, static methods have no access to data stored in specific objects, so no access to this.
Since these methods operate on the class instead of instances of the class, they are called on the class.
Static methods can be overriden.
You can call a static method from another static method within the same class with this.
prototype-based inheritance, super calls, constructors, instance and static methods

# Static properties 

static get Leader(){
  return new User('wat')
}

Note that static properties are a separate concept from static methods, and are still under development.

# Prototypes in JS 
https://stackoverflow.com/a/7694583


# Static methods

function Clazz() {};
Clazz.staticMethod = function() {
    alert('STATIC!!!');
};

Clazz.prototype.func = function() {
    this.constructor.staticMethod();
}

# TS transpiled class

var Greeter = /** @class */ (function () {
    function Greeter(message) {
        this.greeting = message;
    }
    Greeter.prototype.greet = function () {
        return "Hello, " + this.greeting;
    };
    return Greeter;
}());

# Static variables vs instance

function Animal(name) {
    Animal.count = Animal.count+1||1;// static variables, use function name "Animal"
    this.name = name; //instance variable, using "this"
}

# Static vs instance method

Animal.showCount = function () {//static method
    alert(Animal.count)
}

Animal.prototype.showName=function(){//instance method
    alert(this.name);
}













Klasa Parent z dwoma statycznymi metodami:
- obiekt child i parent nie mają dostępu do metod
- metody mogą być wywołane tylko z klasy Child i Parent.sayHello()

class Parent {
  static sayHello() {
    this.speak('world');
  }

  static speak(phrase) {
     console.log(phrase);
  }
}

class Child extends Parent {
}

Parent.sayHello();
Child.sayHello();
const parent = new Parent();
parent.sayHello();
const child = new Child()
child.sayHello();



Klasa Parent z niestatycznym sayHello:
- metoda moze być wywołana z obiektów, ale metoda nie ma dostępu do statycznej metody
- metody NIE mogą być wywołane bezpośrednio z klas Child i Parent.sayHello()

class Parent {
  sayHello() {
    this.speak('world');
  }

  static speak(phrase) {
     console.log(phrase);
  }
}

class Child extends Parent {
}

Parent.sayHello();
Child.sayHello();
const parent = new Parent();
parent.sayHello();
const child = new Child()
child.sayHello();



Klasa Parent ze statyczną metodą korzystająca ze statycznej metody dziecka:
- Parent nie ma dostępu, ale Child ma
- ani child, ani parent nie mają dostępu do sayHello

class Parent {
  static sayHello() {
    this.speak('world');
  }
}

class Child extends Parent {
  static speak(phrase) {
     console.log(phrase);
  }
}

Parent.sayHello();
Child.sayHello();
const parent = new Parent();
parent.sayHello();
const child = new Child()
child.sayHello();


Klasa Parent z metodą korzystająca ze statycznej metody dziecka:
- ani Child, Parent nie ma dostępu do sayHello
- ani child, ani parent nie ma dostepu do speak

class Parent {
  sayHello() {
    this.speak('world');
  }
}

class Child extends Parent {
  static speak(phrase) {
     console.log(phrase);
  }
}

Parent.sayHello();
Child.sayHello();
const parent = new Parent();
parent.sayHello();
const child = new Child()
child.sayHello();



Klasa Parent z metodą korzystająca z metody dziecka:
- tylko child moze bez bledow wywolac metode sayHello

class Parent {
  sayHello() {
    this.speak('world');
  }
}

class Child extends Parent {
  speak(phrase) {
     console.log(phrase);
  }
}

Parent.sayHello();
Child.sayHello();
const parent = new Parent();
parent.sayHello();
const child = new Child()
child.sayHello();



Wnioski:
- bezpośrednio z klas mamy dostęp do metod statycznych, do innych metod nie
- obiekty natomiast nie mają dostępu do metod statycznych