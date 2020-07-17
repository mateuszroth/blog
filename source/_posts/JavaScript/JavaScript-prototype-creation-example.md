---
title: JavaScript prototype creation example
tags:
  - JavaScript
categories:
  - [JavaScript, Basics]
date: 2020-07-17 21:25:00
---
Stwórzmy nową klasę korzystającą z dziedziczenia prototypowego, a następnie utwórzmy nowy obiekt klasy `Person`:
```js
function Person (name) {
  console.log(this);
  this.name = name;
  this.hello();
}
Person.prototype.hello = function () { console.log(this.name) };
new Person('Matt'); // --> wskazuje na Person
// "Matt"
```
Gdy nie użyjemy operatora `new` nie jest tworzony nowy obiekt i używany jest kontekst wywołania funkcji, co zwraca błąd:
```js
function Person (name) {
  console.log(this);
  this.name = name;
  this.hello();
}
Person.prototype.hello = function () { console.log(this.name) };
Person('Matt'); // --> wskazuje na Window - ta linijka inna, bez new
// VM973:3 Uncaught TypeError: this.hello is not a function
//    at Person (<anonymous>:3:8)
//    at <anonymous>:6:1
```
Teraz użyjmy arrow function dla funkcji dodanej do prototypu:
```js
function Person (name) {
  console.log(this);
  this.name = name;
  this.hello();
}
Person.prototype.hello = () => console.log(this.name)  // ta linijka inna, używamy arrow function 
new Person('Matt'); // --> wskazuje na Person
```
Jednak nadal otrzymujemy ten sam błąd gdy pominiemy operator `new`:
```js
VM231:4 Uncaught TypeError: this.hello is not a function
    at Person (<anonymous>:4:8)
    at <anonymous>:7:1
```