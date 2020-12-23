---
title: 'Notes on Swift'
tags:
  - Mobile
  - Swift
  - iOS
categories:
  - [Mobile, Swift, iOS]
date: 2020-12-22 20:00:00
---
## Combine
### Combine schedulers `.receive` and `.subscribe`
Combine allows for publishers to specify the scheduler used when either receiving from an upstream publisher (in the case of operators), or when sending to a downstream subscriber. This is critical when working with a subscriber that updates UI elements, as that should always be called on the main thread.
```swift
somePublisher
    .subscribe(on: DispatchQueue.global()) // to subscribe on background thread
    .receive(on: RunLoop.main) // but receive results on main thread as we need it for some UI updates
    ...
```

### `Future` with `Deferred`
If you want your `Future` to act more like Rx's `Single` by having it defer its execution until it receives a subscriber, and having the work execute every time you subscribe you can wrap your `Future` in a `Deferred` publisher. Let's expand the previous example a bit to demonstrate this:
```swift
func createFuture() -> AnyPublisher<Int, Never> {
    return Deferred {
        Future { promise in
            print("Closure executed")
            promise(.success(42))
        }
    }.eraseToAnyPublisher()
}

let future = createFuture()  // nothing happens yet

let sub1 = future.sink(receiveValue: { value in 
  print("sub1: \(value)")
}) // the Future executes because it has a subscriber

let sub2 = future.sink(receiveValue: { value in 
  print("sub2: \(value)")
}) // the Future executes again because it received another subscriber
```
source: https://www.donnywals.com/using-promises-and-futures-in-combine/

## SwiftUI
### Aligning with `.alignmentGuide`
To make for example one text align to the left and one to the right within a container, you can use `alignmentGuide` as below.
```swift
    VStack(alignment: .leading) {
        Text("Hello, world!")
            .alignmentGuide(.leading) { d in d[.trailing] }
        Text("This is a longer line of text")
    }
        .background(Color.red)
        .frame(width: 400, height: 400)
        .background(Color.blue)
```
![SwiftUI alignmentGuide example](Mobile/Images/SwiftUI-alignmentGuide.png)

source: https://www.hackingwithswift.com/books/ios-swiftui/alignment-and-alignment-guides

## Async code. DispatchQueue
### Use DispatchQueue to print something after 1 second
```swift
DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
    print("Timer fired!")
}
```

## Timer
### Basic usage of scheduled timer
```swift
var runCount = 0

Timer.scheduledTimer(withTimeInterval: 1.0, repeats: true) { timer in
    print("Timer fired!")
    runCount += 1

    if runCount == 3 {
        timer.invalidate()
    }
}
```


### Example of using Timer within SwiftUI's `ObservableObject`
```swift
class TimeCounter: ObservableObject {
    @Published var time = 0
    
    lazy var timer = Timer.scheduledTimer(withTimeInterval: 1, repeats: true) { _ in self.time += 1 }
    init() { timer.fire() }
}

struct ContentView: View {
    @StateObject var timeCounter = TimeCounter()
    
    var body: some View {
        Text("\(timeCounter.time)")
    }
}
```

## Swift language quirks
### `Self` vs `self`
When used with a capital S, `Self` refers to the type that conform to the protocol, e.g. `String` or `Int`. When used with a lowercase S, `self` refers to the value inside that type, e.g. `“hello”` or `556`.
```swift
extension BinaryInteger {
    func squared() -> Self {
        return self * self
    }
}
```


### `class func` vs `static func` functions
Protocols use the `class` keyword, but it doesn't exclude structs from implementing the protocol, they just use `static` instead. Class was chosen for protocols so there wouldn't have to be a third keyword to represent `static` or `class`. That's the main difference but some other differences are that class functions are dynamically dispatched and can be overridden by subclasses.

```swift
class ClassA {
    class func func1() -> String {
        return "func1"
    }

    static func func2() -> String {
        return "func2"
    }

    /* same as above
    final class func func2() -> String {
        return "func2"
    }
    */
}

class ClassB : ClassA {
    override class func func1() -> String {
        return "func1 in ClassB"
    }

    // ERROR: Class method overrides a 'final` class method
    override static func func2() -> String {
        return "func2 in ClassB"
    }
}
```
