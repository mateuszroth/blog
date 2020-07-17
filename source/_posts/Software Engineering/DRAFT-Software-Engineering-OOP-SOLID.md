---
title: "[DRAFT] OOP - SOLID"
tags:
  - Software Engineering
categories:
  - [Software Engineering, OOP]
date: 2019-01-01 10:00:00
---

[Examples with JS code](https://blog.bitsrc.io/solid-principles-every-developer-should-know-b3bfa96bb688)

# S - SRP - Single Responsibility Principle

- class should have just a one purpose - so for example `Animal` class shouldn't perform logs to different outputs or shouldn't perform a role of database of animals
- don't:

```ts
class Animal {
    constructor(name: string) {}
    getAnimalName() {}
    saveAnimal(a: Animal) {}
}
```

- do:

```ts
class Animal {
    constructor(name: string) {}
    getAnimalName() {}
}
class AnimalDB {
    getAnimal(a: Animal) {}
    saveAnimal(a: Animal) {}
}
```
- animal class shouldn't be responsible for database management like saving

# O - OCP - **Open/Closed Principle**

- classes should be open for extensions (new methods) but **closed for modifications** (don't change method) - I'd say, you can change methods but not the contract what they receive and return
- I'd say this role is more about abstraction and use of inheritance, for example by having a base class `Animal` with method `makeSound`, which is going to be implemented by child classes `Lion` or `Snake`
- don't:

```ts
//...
function AnimalSound(a: Array<Animal>) {
    for(int i = 0; i <= a.length; i++) {
        if(a[i].name == 'lion')
            log('roar');
        if(a[i].name == 'mouse')
            log('squeak');
        if(a[i].name == 'snake')
        log('hiss');
    }
}
AnimalSound(animals);
```

- You see, for every new animal, a new logic is added to the AnimalSound function. This is quite a simple example. When your application grows and becomes complex, you will see that the `if` statement would be repeated over and over again in the `AnimalSound` function each time a new animal is added, all over the application. Do instead:

```ts
class Animal {
    makeSound();
    //...
}
class Lion extends Animal {
    makeSound() {
        return 'roar';
    }
}
class Squirrel extends Animal {
    makeSound() {
        return 'squeak';
    }
}
class Snake extends Animal {
    makeSound() {
        return 'hiss';
    }
}
//...
function AnimalSound(a: Array<Animal>) {
    for(int i = 0; i <= a.length; i++) {
        log(a[i].makeSound());
    }
}
AnimalSound(animals);
```

- another example:

```js
class Discount {
    giveDiscount() {
        if (this.customer == "fav") {
            return this.price * 0.2;
        }
        if (this.customer == "vip") {
            return this.price * 0.4;
        }
    }
}
```

- do instead:

```ts
class Discount {
    giveDiscount() {
        return this.price * 0.2;
    }
};

class VIPDiscount: Discount {
    getDiscount() {
        return super.getDiscount() * 2;
    }
};
```

# L - LSP - **Liskov Substitution Principle**

- if something uses a class, it should be able to use the class and the base class / child class of it
- sub-class must be substitutable for its super-class
- PL: nie sprawdzamy typu klasy, wykorzystujemy metody wirtualne i implementujemy je różnie w róznych klasach, ale wywołujemy tak samo

# I - ISP - **Interface Segregation Principle**

- you should write few interfaces instead of a big one interface that contains all the interfaces
- make fine grained interfaces that are client specific
- clients should not be forced to depend upon interfaces that they do not use
- PL: nie tworzymy metod, których nie będziemy mogli zaimplementować w klasach korzystających z interfejsu, np. przykład z `draw` vs `drawCircle`, `drawTriangle`

# D - DIP - Dependency Inversion Principle

- you should create new class by placing in the constructor of it the interface of a class that the new class depends on
- PL: polegamy na interfejsach, nie ich implementacjach - aby można było podmienić lub zamockować
