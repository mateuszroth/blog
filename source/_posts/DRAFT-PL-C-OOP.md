---
title: '[DRAFT] [PL] C# & OOP'
tags:
  - C#
  - OOP
categories:
  - [Software Engineering, OOP]
date: 2019-01-01 10:00:00
---

Poniższe notatki to głównie skrót i spis pojęć z kursu dostępnego na stronie [https://www.plukasiewicz.net/CSharp_dla_poczatkujacych/Ogolnie_o_jezyku](https://www.plukasiewicz.net/CSharp_dla_poczatkujacych/Ogolnie_o_jezyku) i [https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Atrybuty](https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Atrybuty) , uzupełniony o inne źródła.

## Cechy C#:
<!--kg-card-begin: markdown-->

*   warunki logiczne (boolean conditions)
*   garbage collector

    *   TODO: jak działa?

*   standardowe biblioteki

    *   TODO: na przykład jakie?

*   właściwości i zdarzenia (properties, events)
*   delegaty oraz zarządzanie zdarzeniami (Delegates, Events Management)
*   łatwość używania typów generycznych (Generics)
*   kompilacja warunkowa
*   wielowątkowość
*   LINQ i wyrażenia lambda (lambda expressions)
*   deklaracje przestrzeni nazw
<!--kg-card-end: markdown--><!--kg-card-begin: hr-->

* * *
<!--kg-card-end: hr-->

# Część 1

[https://www.plukasiewicz.net/CSharp_dla_poczatkujacych/Ogolnie_o_jezyku](https://www.plukasiewicz.net/CSharp_dla_poczatkujacych/Ogolnie_o_jezyku)

## Notatki z C#:

*   główna metoda całego programu to `Main`

**Podstawowe części języka:**

*   instrukcje i wyrażenia
*   komentarze
*   kompilowanie i wykonywanie
*   słowa kluczowe

**Typy:**

*   typy wartościowe (value types) - w tym również struct
*   typy referencyjne (reference types)
*   typy wskaźnikowe (pointer types)
*   konwersja niejawna (implicit type conversion)
*   konwersja jawna (explicit type conversion)
*   zmienne, typy integralne (integral types)
*   typy zmiennoprzecinkowe (floating point types)
*   typy dziesiętne (decimal types)
*   typy logiczne (boolean types)
*   typy puste (nullable types)

**Stałe i literały:**

*   Stałe odnoszą się do wartości, których program nie może zmieniać w trakcie wykonywania. Te stałe wartości nazywane są również literałami. Stałe traktowane są jak zwykłe zmienne z zaznaczeniem, że ich wartości nie mogą być modyfikowane.
*   literały całkowite (integer literals)
*   literały zmiennoprzecinkowe (floating-point literals)
*   literały znakowe (character literals)
*   literały łańcuchowe (string literals)

**Operatory:**

*   operatory arytmetyczne
*   operatory relacyjne
*   operatory logiczne
*   operatory bitowe
*   operatory przypisania
*   różne inne operatory

**Sterowanie:**

*   instrukcja warunkowa if
*   instrukcja warunkowa if..else
*   zagnieżdżona instrukcja warunkowa if
*   instrukcja wyboru switch
*   zagnieżdżona instrukcja wyboru switch
*   pętla while
*   pętla for
*   pętla do..while
*   polecenie break
*   polecenie continue

**Parametry, inne typy i tablice:**

*   parametry typu wartościowego, referencyjnego, wyjściowego
*   typy puste
*   tablice wielowymiarowe
*   tablice postrzępione
*   klasa `Array`

**Klasy:**

*   **Klasa** może dziedziczyć z jednej klasy, ale może implementować wiele interfejsów
*   **metody** klasy (methods)
*   **pola **klasy (fields)
*   **właściwości **klasy (properties) - Właściwości nie służą do przechowywania wartości. Przy pomocy accesorów **mają dostęp do pól**, które reprezentują.<!--kg-card-begin: hr-->

* * *
<!--kg-card-end: hr-->

**Class member, np. pole lub metoda**

Class members, in C#, are the members of a class that represent the data and behavior of a class.

Class members are members declared in the class and all those (excluding constructors and destructors) declared in all classes in its inheritance hierarchy.

**Class members **can be of the following types:

*   **Constants** representing constant values
*   **Fields** representing variables
*   **Methods** providing services like calculation or other actions on its members
*   **Properties** that define the class features and include actions to fetch and modify them
*   **Events** generated to communicate between different classes /objects
*   **Indexers** that help in accessing class instances similar to arrays
*   **Operators** that define semantics when used in expressions with class instances
*   **Instance constructors** to initialize members of class instances
*   **Static constructor** to initialize the class itself
*   **Destructors** to execute actions necessary to be performed before class instances are discarded
*   Types that are local to the class (nested type)

**Class members are initialized in constructors** which can be overloaded with different signatures. For classes that do not have constructor, **a default constructor that initializes the class members (to default values) will be generated**.

Source: [https://www.techopedia.com/definition/25589/class-members-c-sharp](https://www.techopedia.com/definition/25589/class-members-c-sharp)
<!--kg-card-begin: hr-->

* * *
<!--kg-card-end: hr-->

**Dalej o klasach:**

*   instancje klasy
*   **hermetyzacja/enkapsulacja, **inaczej** **data hiding (or more accurately **encapsulation**)
*   **modyfikatory dostępu** w C# jako część hermetyzacji - public, private, protected, internal, protected internal
*   typy wyliczeniowe **enum - **wartościowy typ danych - wartości, których nie można dziedziczyć oraz przekazać przez dziedzicznie<!--kg-card-begin: code-->

    enum DniTygodnia
    {
        Poniedzialek = 1,
        Wtorek,
        Sroda,
        Czwartek,
        Piatek,
        Sobota,
        Niedziela
    }`</pre><!--kg-card-end: code-->

*   struktury **struct - **W języku C# struktura to **wartościowy** typ danych.<!--kg-card-begin: hr-->

    * * *
    <!--kg-card-end: hr-->

    **Klasy i struktury** mają następujące różnice:

*   klasy są typem referencyjnym a struktury typem wartościowym;
*   struktury nie wspierają dziedziczenia;
*   struktury nie mogą mieć domyślnego konstruktora.<!--kg-card-begin: hr-->

    * * *
    <!--kg-card-end: hr-->

    **Dalej o klasach:**

*   **konstruktor** i **destruktor** klasy
*   **statyczne składniki **klasy

    Składniki statyczne możemy zdefiniować za pomocą słowa kluczowego **static**. Jeżeli zadeklarujemy składową jako statyczną nie ważne jak wiele obiektów klasy utworzymy, **istnieje zawsze tylko jedna kopia składowej statycznej.**

*   **klasa statyczna**

    Możemy utworzyć statyczną klasę. Klasa taka mówi, iż nie została napisana po to, aby tworzyć nowe obiekty. Nawet, gdybyśmy chcieli utworzyć nowy obiekt klasy statycznej kompilator zgłosi błąd. Mogą być wywołane bez tworzenia instancji danej klasy. 

*   dziedziczenie - **inheritance**
*   klasa bazowa i pochodna - **base/parent **and** derived/child class**
*   polimorfizm - **polymorphism**
*   **statyczny polimorfizm, **tj. przeciążanie metod i przeciążanie operatorów
*   **polimorfizm dynamiczny, czyli klasy abstrakcyjne i metody wirtualne**

    Polimorfizm dynamiczny jest realizowany za pomocą klas abstrakcyjnych oraz metod wirtualnych. Metoda może mieć różne implementacje dla różnych klas.
    <!--kg-card-begin: hr-->

    * * *
    <!--kg-card-end: hr-->

    **Klasa abstrakcyjna**. Klasa taka zawiera abstrakcyjne metody, których implementacja zależy od wykorzystania w poszczególnych klasach pochodnych. 

    Poniżej lista zasad, o których należy pamiętać, tworząc klasy abstrakcyjne:

*   nie można utworzyć instancji klasy abstrakcyjnej;
*   nie można zadeklarować metody abstrakcyjnej poza klasą abstrakcyjną;
*   kiedy klasa opatrzona jest modyfikatorem dostępu sealed nie może być dziedziczona. Dodatkowo, klasa abstrakcyjna nie może być zdefiniowana jako sealed.<!--kg-card-begin: hr-->

    * * *
    <!--kg-card-end: hr-->

*   **metody wirtualne**

    Jeżeli masz zdefiniowaną metodę w klasie bazowej, ale chcesz, żeby została zaimplementowana w klasach pochodnych możesz do tego celu zastosować metody wirtualne.

*   **interfejsy**

    Język C# nie obsługuje wielokrotnego dziedziczenia. **Klasa może dziedziczyć po jednej klasie bazowej, ale może implementować wiele interfejsów**.

    **Inne cechy C#:**

*   przestrzenie nazw
*   dyrektywy preprocesora
*   wyrażenia regularne
*   obsługa wyjątków
*   odczyt i zapis pliku<!--kg-card-begin: hr-->

    * * *
    <!--kg-card-end: hr-->

    # Część 2

    [https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Atrybuty](https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Atrybuty)

    **Indeksery:**

*   [https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Indeksery](https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Indeksery)
*   **Indeksery** pozwalają na indeksowanie obiektów w taki sam sposób jak ma to miejsce w tablicach.
*   przeciążanie indekserów

    **Delegaty:**

*   [https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Delegaty](https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Delegaty)
*   **Delegaty** to referencyjny typ danych, który przechowuje referencje do metody.
*   **Delegaty złożone **- Delegat złożony wywołuje dwa delegaty tak jakby były złączone. Operacja taka to tzw. **multicasting**.
*   W JS nie ma typu delegatów, przekazujemy funkcje przez referencje do zmiennej.

    **Zdarzenia:**

*   [https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Zdarzenia](https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Zdarzenia)
*   Klasa, w której definiujemy nasze zdarzenie to tzw. „**publisher**”. Z kolej klasa, która odbiera to zdarzenie to tzw. „**subscriber**”.

    **Kolekcje:**

*   [https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Kolekcje](https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Kolekcje)
*   **ArrayList** reprezentuje uporządkowaną kolekcję obiektu, który może być indeksowany indywidualnie. Wykorzystuje klucz do dostępu do elementu kolekcji.
*   **Kolekcje**: ArrayList, Hashtable, SortedList, Stack, Queue

    **Typy generyczne:**

*   [https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Typy_generyczne](https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Typy_generyczne)
*   **Typy generyczne** pozwalają na opóźnienie w dostarczeniu specyfikacji typu danych w elementach takich jak klasy czy metody do momentu użycia ich w trakcie wykonywania programu. Innymi słowy, typy generyczne pozwalają na napisanie klasy lub metody, która może działać z każdym typem danych.

    **Refleksja:**

*   [https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Refleksja](https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Refleksja)
*   jest możliwe pobranie informacji dotyczących używanych typów w trakcie wykonywania programu – za pomocą **mechanizmu refleksji**.

    **Unsafe code:**

*   [https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Unsafe_code](https://www.plukasiewicz.net/Csharp_dla_zaawansowanych/Unsafe_code)
*   **Kod niezabezpieczony** lub też kod **niekontrolowany** to blok **kodu używający wskaźników**.

    # Część 3

    Inne materiały i informacje

    ## Implicit Interface Implementation vs Explicit Interface Implementation

*   **Implicit**: you access the interface methods and properties as **if they were part of the class**.<!--kg-card-begin: code--><pre>`public class Test : ITest
    {
        public string Id // Generated by Implement Interface
        {
            get { throw new NotImplementedException(); }
        }
    }

    Test t = new Test();
    t.Id; // OK
    ((ITest)t).Id; // OK`</pre><!--kg-card-end: code-->

*   **Explicit**: you can only access methods and properties **when treating the class as the implemented interface**.<!--kg-card-begin: code--><pre>`public class Test : ITest
    {
        string ITest.Id // Generated by Implement Interface Explicitly
        {
            get { throw new NotImplementedException(); }
        }
    }

    Test t = new Test();
    t.Id; // Not OK
    ((ITest)t).Id; // OK

    ITest it = t;
    it.Id; // OK`</pre><!--kg-card-end: code-->

    **_It allows you to implement two interfaces that define the same method_**. However, if you explicitly implement the interface, the methods can only be accessed when the variable is typed to that explicit interface.

    In terms of "when" you have to implement an interface explicitly, it is **when your class already has a method with the same signature** as one of the methods of your interface, or when your class implements **several interfaces that share methods with the same signatures** but incompatible contracts. Source: [https://softwareengineering.stackexchange.com/questions/136319/whats-the-difference-between-implementing-an-interface-explicitly-or-implicitly](https://softwareengineering.stackexchange.com/questions/136319/whats-the-difference-between-implementing-an-interface-explicitly-or-implicitly)

    More about explicit interface implementation: [https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/interfaces/explicit-interface-implementation](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/interfaces/explicit-interface-implementation)

    ## Casting struct to interface

    The fact that a struct can implement an interface is well known and so is the fact that casting a value type into an interface **leads to boxing of the value type.** This is because methods in interfaces are defined as virtual and to resolve virtual references, vtable (method table) look up is required. **Since value types do not have pointers to vtable they are first boxed into a reference type** and then the look up happens. [https://blogs.msdn.microsoft.com/abhinaba/2005/10/05/c-structs-and-interface/](https://blogs.msdn.microsoft.com/abhinaba/2005/10/05/c-structs-and-interface/)

    Po polsku, chodzi o to, że kiedy jako `struct` zaimplementujemy jakiś `interface` , to `struct` będzie zapakowany w dodatkowy obiekt. Metody wywoływane na instancji tego `struct`, który jest rzutowany na `interface` , na przykład:
    <!--kg-card-begin: code--><pre>`Employee employee = new Employee("Cool Guy", 65);
    IPromotion p = employee;
    Console.WriteLine(employee);
    p.promote();
    Console.WriteLine(employee);

    //Cool Guy (65)
    //Cool Guy (65)
<!--kg-card-end: code-->

modyfikują wartości tego dodatkowego obiektu, a nie w oryginalnym obiekcie `employee`. Jeśli zmienimy `struct` na `class` to nie będzie tego boxowania, tworzenia dodatkowego obiektu i wszystko będzie działać jak należy. Wynika to z tego, że:
> **casting a value type into an interface leads to boxing of the value type**
> This is because methods in interfaces are defined as virtual and to resolve virtual references, vtable (method table) look up is required. Since value types do not have pointers to vtable they are first boxed into a reference type and then the look up happens.

więcej tutaj: [https://blogs.msdn.microsoft.com/abhinaba/2005/10/05/c-structs-and-interface/](https://blogs.msdn.microsoft.com/abhinaba/2005/10/05/c-structs-and-interface/)

## Deadlocks

*   TODO: jak dochodzi do deadlocków?
*   **Transaction levels**: snapshot, commitread

## ASP.NET MVC, ASP.NET Core MVC:

*   ASP.NET CORE [https://docs.microsoft.com/pl-pl/aspnet/core/tutorials/first-mvc-app/?view=aspnetcore-2.2](https://docs.microsoft.com/pl-pl/aspnet/core/tutorials/first-mvc-app/?view=aspnetcore-2.2)
*   ASP.NET [https://docs.microsoft.com/pl-pl/aspnet/mvc/overview/getting-started/index](https://docs.microsoft.com/pl-pl/aspnet/mvc/overview/getting-started/index)