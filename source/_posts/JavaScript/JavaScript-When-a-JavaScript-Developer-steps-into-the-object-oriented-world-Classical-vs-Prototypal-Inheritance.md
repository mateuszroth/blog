---
title: >-
  When a JavaScript Developer steps into the object-oriented world |
  Classical vs Prototypal Inheritance
tags:
  - JavaScript
  - OOP
categories:
  - [JavaScript, OOP]
date: 2019-01-01 10:00:00
---
# Links
Benefits of prototypal inheritance over classical?, Aadit M Shah, [https://stackoverflow.com/a/16872315](https://stackoverflow.com/a/16872315)
* delegation inheritance via __proto__
* concatenation inheritance through copying object properties

Why Prototypal Inheritance Matters, Aadit M Shah, [http://aaditmshah.github.io/why-prototypal-inheritance-matters/](http://aaditmshah.github.io/why-prototypal-inheritance-matters/)

Prototypal Inheritance, Douglas Crockford, [http://crockford.com/javascript/prototypal.html](http://crockford.com/javascript/prototypal.html)

Differential inheritance, Wikipedia, [https://en.wikipedia.org/wiki/Differential_inheritance](https://en.wikipedia.org/wiki/Differential_inheritance)

JavaScript The good parts, Douglas Crockford, [https://www.amazon.com/dp/0596517742/?tag=stackoverflow17-20](https://www.amazon.com/dp/0596517742/?tag=stackoverflow17-20)

JavaScript For Beginners: the ‘new’ operator, Brandon Morelli,
[https://codeburst.io/javascript-for-beginners-the-new-operator-cee35beb669e](https://codeburst.io/javascript-for-beginners-the-new-operator-cee35beb669e)

JavaScript: The Keyword ‘This’ for Beginners [https://codeburst.io/javascript-the-keyword-this-for-beginners-fb5238d99f85](https://codeburst.io/javascript-the-keyword-this-for-beginners-fb5238d99f85)

old vs new JS inheritance class: [https://medium.com/beginners-guide-to-mobile-web-development/super-and-extends-in-javascript-es6-understanding-the-tough-parts-6120372d3420](https://medium.com/beginners-guide-to-mobile-web-development/super-and-extends-in-javascript-es6-understanding-the-tough-parts-6120372d3420)

JS class inheritance: [https://javascript.info/class-inheritance](https://javascript.info/class-inheritance)

https://stackoverflow.com/a/18557503 in this article:

*   - why encapsulation is good presented on an example of online shop (discounts, changed to max 80%, for some resellers 90%)
*   - This is also a bad design, a boilerplate antipattern
*   property vs private member/field
*   - In C#, transforming fields into properties is a breaking change, so public fields should be coded as Auto-Implemented Properties if your code might be used in separatedly compiled client.
*   In Javascript, the standard properties (data member with getter and setter described above) are defined by accessor descriptor (in the link you have in your question). Exclusively, you can use data descriptor (so you can't use i.e. value and set on the same property).

new keyword vs Object.create: [https://stackoverflow.com/questions/4166616/understanding-the-difference-between-object-create-and-new-somefunction](https://stackoverflow.com/questions/4166616/understanding-the-difference-between-object-create-and-new-somefunction)

How to not use prototype, _<em>generalization is always better than specialization_</em>: [https://stackoverflow.com/a/21807662](https://stackoverflow.com/a/21807662)

# Classical inheritance in object-oriented system like C# and Java

I believe you already heard about classes and you know some basics like new objects are created during instantiation from classes. But classical inheritance is much more complicated and have terms that not exists in JavaScript:

*   classes
*   objects
*   interfaces
*   abstract classes
*   final classes
*   virtual base classes
*   constructors
*   destructors

They were defined to achieve terms like:

*   encapsulation
*   inheritance
*   polymorphism

[https://stackoverflow.com/questions/816071/prototype-based-vs-class-based-inheritance](https://stackoverflow.com/questions/816071/prototype-based-vs-class-based-inheritance)
Object oriented:
- encapsulation
- inheritance
- polymorphism

## Comparison of OOP vs Prototypal

- in a “class-based” language, that copying happens at compile time
- in prototypal, there is no copying, we have reference to prototype and it’s methods
- instantiation vs copying reference to prototype

### Prototypal inheritance in JS

In a prototypal system, objects inherit from objects by the mechanism which is looking for methods in `__proto__`. The `__proto__` property is created on object when instantiated by using `new` keyword. When you define a new function or class, it has `prototype` defined instead.

For example, let's say we have `Woman` class which inherits from `Human` class in JavaScript. When you instantiate a `Woman` object then it would have `__proto__` pointing to `Human`. All class members defined in `Human` but not in `Woman` will be accessible in the instance of the `Woman` class because the object will look first in it's own members for example for invoked method and if it is not present, it will go to `__proto__` and check if it's is there, if not then it would go to `__proto__` of `__proto__` and so on.

### “Instantiation” in JavaScript

First way to instantiate an object is to do it from constructor function. It’s a function like every other function but we can define for it the `prototype` property which will be used as a `__proto__` property for newly created object by using `new` keyword.

Ok, let’s slow down. First look how we declare constructor function:

```
function Person() {}
```

Yes, you’re right. It’s a function like every other function. Good practice is to start constructor function name from upper case to distinguish it from normal function but it’s not necessary.

What is prototype of this function? By default it’s object which inherits from `Object` , so it’s `__proto__` property is set to `Object` . Also it has additional property `constructor`:
```
Person.prototype
// { constructor: f, __proto__: Object }
```

But what is `constructor`? It’s property which points to our function which in our case is `Person` :
```
{
  constructor: Person,
    __proto__: Object
}
```

I believe you already understand what’s the purpose of `__proto__` . But what’s the purpose of `constructor` ? It will just say us what function was used to create an object.

So let’s create a simple constructor function:
```
function Person(name) {
  this.name = name;
  console.log(this);
  console.log(this.prototype);
  console.log(this.__proto__);
}
Person.prototype.sayHello = function () { console.log(this.name); };
const matt = new Person('Matt');
matt.sayHello();
// 'Matt'
```

`prototype` is an object with `constructor` property that references to the constructor function (`Person`). Every function has prototype with this property which points to that function:
```
function getHello () { return 'Hello World' };
getHello.prototype.constructor === getHello;
// true
```

`prototype` is not available on the instances themselves (or other objects), but only on the constructor functions.

The `constructor` property returns a reference to the `Object` constructor function that created the instance object.
```
function Person(name) {
  this.name = name;
}
var person = new Person('Matt');
person.constructor
// function Person...
console.log(person.prototype)
// undefined
console.log(Person.prototype)
// { constructor: ...
```

`Object.create` creates a new object which has it’s prototype set to the passed in object, i.e.:
```
const obj = {};
const obj2 = Object.create(obj);
obj2.__proto__ === obj;
// true
```

The `Object.create` function untangles JavaScript’s constructor pattern, achieving true prototypal inheritance.

So instead of creating classes, you make prototype objects, and then use the `Object.create` function to make new instances.
```
class Person {
  constructor(name) {
    this.name = name;
    console.log(this);
    console.log(this.prototype);
  }
  sayHello() {
    console.log(this.name);
  }
}
```

```
function Person(name) {
  this.name = name;
  console.log(this);
  console.log(this.prototype);
}
Person.prototype.sayHello = function() {
  console.log(this.name);
}
Person(‘Matt’); // this wskazuje na window, przypisuje zatem ‘Matt’ do window.this
new Person(‘Matt’); // this wskazuje na aktualny kontekst funkcji Person
Object.create(Person); // tworzy kopię obiektu — funkcję, która jest kopią funkcji Person — prototypem jest funkcja Person
Object.create(Person.prototype); // tworzy kopię obiektu na podstawie prototypu — prototypem jest obiekt Person
```


```
function Person(name) {
  this.name = name;
  console.log(this);
  console.log(this.prototype);
  this.sayHello = function() {
  console.log(this.name);
  }
}
```

- new zatem tworzy obiekt, który wskazuje na kontekst funkcji jako this
- bez new, nie jest utworzony prototyp, a this wskazuje na window

```
Person(‘matt’)
&gt;&gt; Uncaught TypeError: Class constructor Person cannot be invoked without ‘new’
typeof Person
&gt;&gt; “function”
const matt = Object.create(Person(“Matt”))
&gt;&gt; Uncaught TypeError: Class constructor Person cannot be invoked without ‘new’
```

* klasa ma typ funkcji
* nie można wywoływać klas bez użycia `new`
* klasa zwraca nowy obiekt
* można utworzyć kopię obiektu zwracanego przez klasę za pomocą Object.create, tak skopiowany obiekt nie ma prototypu/this jeśli klasa go nie miała


## ES6 class vs old function constructor approach

Let's say we have a `Human` class:
```
class Human {
  constructor (name) {
    this.name = name; 
  }
}

const human = new Human('Homo sapiens');
```

As function this would be:
```
function HumanFn(name) {
  this.name = name;
}
const humanFn = new HumanFn('Homo sapiens');
```

As you can see, in the function approach we can instantiate an object from a function. Basically what `new` operator does in JS is it is creating a new object, sets the constructor of the object to the function (which is `HumanFn`), calls the constructor with the context of the newly created object and returns `this` if the constructor (function `HumanFn`) does not return nothing otherwise the thing that the constructor returns.

Let's compare them once more in deep:
```
class Person {
  constructor(name) {
        this.name = name;
    }
}

const matt = new Person('Matt'); // works
const john = new matt.constructor('John'); // works the same as above
const tom = matt.constructor('Tom'); // error `Class constructor Person cannot be invoked without 'new'`
```

In function approach it is slightly different:
```
function Person(name) {
  this.name = name;
}

const matt = new Person('Matt'); // works
const john = new matt.constructor('John'); // works as above
const tom = Person('Tom'); // tom is undefined
const tom2 = matt.constructor('Tom'); // tom2 is undefined`
```

The difference is in line related to `tom`. `Person` is called as a function. Context of the invoked function is set to `window` instead of to a new object created by the `new` keyword as in previously created `matt` or `john`. 

## Inheritance comparision

We have ES6 class extended:
```
class Human {
  constructor (name) {
  this.name = name;
  }
  sayName () { console.log(this.name) };
}

class Woman extends Human {
  gender = 'female'
}

const eva = new Woman('Eva');
```

We do not need constructor above because if you do not specify a constructor method a default empty constructor is used. For derived classes, the default constructor is:
```
constructor(...args) {
  super(...args);
}
```

As function this would be:
```
function HumanFn(name) {
  this.name = name;
}
HumanFn.prototype.sayName = function() { console.log(this.name) }

function WomanFn(name) {
    HumanFn.call(this, name);
    this.gender = 'female';
}
WomanFn.prototype = Object.create(HumanFn.prototype);

const evaFn = new WomanFn('Eva');
```

Instead of using `extends`, you need to set `WomanFn` prototype manually.












---

*   you can't use `call` on not instantiated `class`, it will return error `Class constructor Human cannot be invoked without 'new'`
*   `static` methods can be called only on not instantiated `class`, no need to instantiate
*   `static` methods are not available on instantiated `class`
*   `static` methods has no access to `this`, but we can call them for example by using `Human.sayHello.call(instantiatedHumanObject)`
*   As stated, if you do not specify a constructor method a default empty constructor is used. For derived classes, the default conxstructor is:<!--kg-card-begin: code--><pre>`constructor(...args) {
      super(...args);
    }


## Object methods

*   `Object.defineProperty(objectOrContext, propertyName, propertyDescriptors)`*   descriptors: `configurable`, `enumerable`, `writable`, `set`, `get`, `value`
*   accessors: `get`, `set`
*   `Object.setPrototypeOf(obj2, obj1)`
*   `Object.getPrototypeOf(object)`
*   `Object.getOwnPropertyNames(object)`
*   `Object.getOwnPropertyDescriptor(object, property)`
*   `Object.defineProperties(object, descriptors)`
*   prevents adding properties to an object: `Object.preventExtensions(object)`, `Object.isExtensible(object)`*   prevents changes of object properties (not values): `Object.seal(object)`, `Object.isSealed(object)`
*   prevents any changes to an object: `Object.freeze(object)`, `Object.isFrozen(object)`