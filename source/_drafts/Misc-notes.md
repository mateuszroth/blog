---
title: Misc notes
tags:
  -
categories:
  - []
date: 2020-07-17 20:00:00
---

# New Web APIs
## Device Orientation and Motion online
- https://developers.google.com/web/fundamentals/native-hardware/device-orientation/
```js
if (window.DeviceOrientationEvent) {
  window.addEventListener('deviceorientation', deviceOrientationHandler, false);
  document.getElementById("doeSupported").innerText = "Supported!";
}

if (window.DeviceMotionEvent) {
  window.addEventListener('devicemotion', deviceMotionHandler);
  setTimeout(stopJump, 3*1000);
}
```

## Generic Sensor API
- https://developers.google.com/web/updates/2017/09/sensors-for-the-web

## Broadcast Channel API

--------------------------------------------------------------------------------------------------------------------

# Frontend

## Rollup vs Webpack vs Parcel
- Rollup: https://code.lengstorf.com/learn-rollup-js/

## CSS
- new CSS props: clip, will-change, pointer-events

--------------------------------------------------------------------------------------------------------------------

# Tests
- Stub słuzy do mockowania funkcji, ktore beda zwracaly okreslona wartosc (do zastepowania konkretnych funkcjami swoimi).
```js
const getPurchaseOrderSampleStub = sandbox.stub(props, 'getPurchaseOrderSample', () => {
  return 'image'
})
wrapper.instance().setPaperworkData()
expect(wrapper.state('purchaseOrderSampleImage')).to.be.equal('image')
```
- fakes
- sandbox / sinon
- spy
- afterEach restore
- shallow
- expect
- wrapper

--------------------------------------------------------------------------------------------------------------------

# PROGRAMMING
# DAMP vs DRY
https://stackoverflow.com/questions/6453235/what-does-damp-not-dry-mean-when-talking-about-unit-tests

# REBASE
But again, this only works for private feature branches. If you’re collaborating with other developers via the same feature branch, that branch is public, and you’re not allowed to re-write its history.
https://www.atlassian.com/git/tutorials/merging-vs-rebasing

If the conflicts are too bad and you need to bail out and attempt a normal fast-forward merge, you can easily do so with git rebase --abort (leaving you where you were before attempting the rebase).
So, always try rebase first, and your git history will thank you (and take note, there is git pull --rebase as well- I won’t go into the whole fetch/merge vs. pull flamewar here).
https://nathanleclaire.com/blog/2014/09/14/dont-be-scared-of-git-rebase/


# ARCHITEKTURA, WSPÓŁPRACA, MYŚLI
- Co jest dla nas ważniejsze: praca developerów i codebase czy wydajność aplikacji?
- Unikanie centralności, modułowość codebase - łatwość edycji i wdrażania nowych funkcji
- Uważanie z abstrakcją, która kosztuje

# parameter vs argument
A parameter is a variable in a method definition. When a method is called, the arguments are the data you pass into the method's parameters. Parameter is variable in the declaration of function. Argument is the actual value of this variable that gets passed to function.
https://stackoverflow.com/a/156787

--------------------------------------------------------------------------------------------------------------------

# JAVASCRIPT
# Partial Application
https://github.com/tc39/proposal-partial-application

# Pipeline operator
https://github.com/tc39/proposal-pipeline-operator
```
function doubleSay (str) {
  return str + ", " + str;
}
function capitalize (str) {
  return str[0].toUpperCase() + str.substring(1);
}
function exclaim (str) {
  return str + '!';
}
let result = exclaim(capitalize(doubleSay("hello")));
result //=> "Hello, hello!"

let result = "hello"
  |> doubleSay
  |> capitalize
  |> exclaim;

result //=> "Hello, hello!"
```

# Nullish coalescing
```
value != null ? value : 'default value';
value || 'default value'
value != null
value !== null && value !== undefined
value ?? 'default value';
```

# ARRAY
Array.from(Array(5).keys())
[...Array(5).keys()]
Array.from(new Array(20), (x,i) => i)
Array(10).fill(1).map((x, y) => x + y)

ES6+
```
let [key, message] = params.split(';')
let { name, age } = { name: 'mateusz', age: 11 }
```
* statyczne metody i pola klas: http://www.react.express/static_class_properties "We can use the static keyword to declare static class functions. Static method calls are made directly on the class and cannot be called on instances of the class."
* Class Instance Properties - bez konieczności definiowania
* Bound Instance Methods
* Object Spread
* Async and Await - We can use the async keyword before a function name to wrap the return value of this function in a Promise. We can use the await keyword (in an async function) to wait for a promise to be resolved or rejected before continuing code execution in this block.

--------------------------------------------------------------------------------------------------------------------

# REACT
# React async mode:
- low i high priority (low np. fetch, high np. onChange inputu)
- async mode wprowadza low i high priority reconcilation. React będzie używał heurystyki żeby określić czy dany setState jest high priority (np. odpowiedź na onChange inputu) czy low priority (np. wykonanie się promisa pobierającego dane) i faktyczny stan może być różny na różnych gałęziach drzewa (szczególnie jak jeszcze dodasz do tego Suspense). 
- Takie zachowanie może powodować tzw. "tearing" czyli niespójność UI - np. po zalogowaniu się nagłówek może pokazywać, że user jest zalogowany, a content pokazywać jeszcze informacje z formularzem logowania przez kilka ms/s.
- Dodatkowo, prowadzi to do większego nakładu pracy jaki React musi wykonać w commit phase (obliczanie VDOM) jeżeli przed powiązanym z nim flushem (aktualizacja faktycznego stanu + DOM) nastąpi kolejny setState.
- typowe flow w naszej apce Rx przy np. głupim pobraniu tabel i ich wyświetleniu
0. guard by wejść na stronkę (najczęściej)
1.user klika button pobierz
2.emit event z 'głupiego' komponentu do kontenera
3.kontener odpala metodę serwisu dla kontenera 
4.metoda robi dispatch akcji init pobierz z api
5.efekt odpalający komunikację z api
6.api pobierające i parsowanie danych
7. akcja success lub fail
8. akcja notyfikacji success lub fail 
9. efekt odpalający notyfikacje success lub fail
10. akcja zapisz do store
11. reducer zapisujący do store
12. selektor tabel ze store
13. serwis kontenera korzystający z selektora
14. kontener pobiera tabele z serwisu
15. kontener przekazuje do głupiego komponentu
16. głupi komponent wyświetla tabele na stronie
Do wszystkiego unit testy

# REACT BASICS
ewaluacja wartości i typów -> porównywanie liczby z obiektem, wywoła na obiekcie valueOf lub toString
https://github.com/reactjs/react-basic

* Transformation
** The core premise for React is that UIs are simply a projection of data into a different form of data.
* Abstraction
* Composition
* State
* Memoization
* Lists (maps)

```js
componentWillMount() {
  window.performance.mark('App')
}

componentDidMount() {
  console.log(window.performance.now('App'))
}
```
https://engineering.musefind.com/how-to-benchmark-react-components-the-quick-and-dirty-guide-f595baf1014c


Ciekawe rzeczy o czasu poswieconym na PropTypes podczas developmentu:
https://benchling.engineering/performance-engineering-with-react-e03013e53285

--------------------------------------------------------------------------------------------------------------------

# TYPESCRIPT
- generyczne
- null checking
- interfejsy
- namespace
- partiale
- type guard
- generic types
- reducers, actions, effects

`transpileOnly`; niedługo pewnie też przestawimy `implicitAny` na false i `strictNullChecking` na true

To może tak: łatwiej jest refaktorować kod z testami czy bez? Z dokumentacją czy bez? TypeScript to w części właśnie takie nisko-poziomowe testy i dokumentacja.

Żeby przetestować, czy wszystkie metody w każdej sytuacji dostają dane oczekiwanych typów i zwracają oczekiwane typy.

To jest de facto nierobialne ręcznie na taką skalę, jaką TypeScript daje out of the box.

One generalnie są stabilne i oferują różne podejście do typowania. Z czego żadne nie jest obiektywnie najlepsze, a dobór powinien zależeć od wymagań

nie ma żadnego problemu z TS. Jest to vendor lock i ryzyko. To, że obecnie relatywnie łatwo z tego wyjść, a na horyzoncie widmo klapy nie widnieje, nie znaczy, że nie należy tego wkalkulować w proces decyzyjny. Każda decyzja dotycząca stacku niesie ze sobą ryzyko i należy być tego świadomym. To samo dotyczy choćby Flow, czy praktycznie każdej nietrywialnej biblioteki. Nasz ekosystem taki jest i tyle.

To powyższe to komunały, ale wniosek już taki banalny nie jest -- należy projektować architekturę tak, aby poszczególne jej elementy były wymienialne. Odpowiedzią na pytanie "jak wykopać dół, który nie zmieni się w szambo?" jest "wykopać wiele małych dołków", a nie "użyjmy teraz szpadelka tej innej firmy i może tym razem się uda".

Ale wracając do sedna, wydaje mi się, że mając "standardowy" projekt reactowy, o wiele łatwiej jest dorzucić do stacka Flow, niż TS, który powiela odpowiedzialności z Babelem. W dodatku ze znanych mi implementacji TSa wyłaniają się docelowo dwie wersje:

- programiści mają (za) dużo czasu -- cały codebase zmierza do 100% TypeScript approved. Zrobienie głupiego proof of conceptu staje się koszmarem, bo do byle pierdoły musisz pisać/zmieniać tonę interfejsów, które jedyne co robią, to pozornie zabezpieczają Cię przed tym, że Twój kolega z teamu może być idiotą, któremu nikt nie jest w stanie zrobić code review ;)

- programiści nie mają (za) dużo czasu -- "yyy, nie działa, ch*j, : any" (i tak razy milyjard)
--------------------------------------------------------------------------------------------------------------------