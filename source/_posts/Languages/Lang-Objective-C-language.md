---
title: 'Objective C programming language attributes'
tags:
  - Software Engineering
  - Programming languages
  - Objective C
categories:
  - [Software Engineering, Programming languages]
date: 2020-07-17 20:00:00
---
## Wypisywanie w konsoli:
```objc
NSLog(@"%@", strValue);
NSLog(flag ? @"Yes" : @"No");
```
* For Strings you use `%@`
* For int  you use `%i`
* For float and double you use `%f`
* For bool you use `%d`

## Consty i zmienne:
```objc
  const char NEWLINE = '\n';
  int area;  
```

## Tworzenie klas i obiektów:
```objc
@interface SampleClass:NSObject
- (void)sampleMethod;
@end

@implementation SampleClass
- (void)sampleMethod {
   NSLog(@"Hello, World! \n");
}
@end

int main() {
   /* my first program in Objective-C */
   SampleClass *sampleClass = [[SampleClass alloc]init];
   [sampleClass sampleMethod];
   return 0;
}
```

## Tworzenie `struct`:
```objc
struct Books {
   NSString *title;
   NSString *author;
   NSString *subject;
   int   book_id;
};
```

### Manipulowanie `struct`:
```objc
@interface BookLogger:NSObject
/* function declaration */
- (void) printBook:(struct Books*) book;
@end

@implementation BookLogger
- (void) printBook:(struct Books*) book {
   NSLog(@"Book title: %@\n", book->title);
   NSLog(@"Book author: %@\n", book->author);
   NSLog(@"Book subject: %@\n", book->subject);
   NSLog(@"Book book_id: %d\n", book->book_id);
}
@end

int main() {
   struct Books Book1;        /* Declare Book1 of type Book */
   struct Books Book2;        /* Declare Book2 of type Book */

  BookLogger *bookLogger = [[BookLogger alloc]init];
  /* print Book1 info */
  [sampleClass bookLogger: Book1];
}
```

## Tworzenie bloków funkcji:
```objc
- (return_type) method_name:(argumentType1)argumentName1 
joiningArgument2:(argumentType2)argumentName2 ... 
joiningArgumentn:(argumentTypen)argumentNamen {
   body of the function
}
```
i.e.:
```objc
double (^multiplyTwoValues)(double, double) = 
   ^(double firstValue, double secondValue) {
      return firstValue * secondValue;
   };

double result = multiplyTwoValues(2,4); 
NSLog(@"The result is %f", result);
```

## Struktury danych:
* `NSDictionary` could be accessed like `dict[@"key"]` or `[dict objectForKey:@"key"]`
* `NSArray` is accessible via indexes: 0, 1, 2 etc:

### Inicjacja `NSArray`:
```objc
NSArray* array = @[@"One", @"Two", @"Three"];
NSArray* array = @[Object1, Object2]
```

### Iterowanie po `NSDictionary`:
```objc
for (NSString* key in yourDict) {
    NSLog(@"%@", yourDict[key]);
    //or
    NSLog(@"%@", [yourDict objectForKey:key]);
}
```

### Inicjalizacja `NSDictionary`:
```objc
NSDictionary* dict = @{ key : value, key2 : value2};
```

#### Dodawanie do `NSDictionary` wartości niebędającej obiektem wymaga jej rzutowania na odpowiedni obiekt Objective C:
```objc
@"facebookId": [NSNumber numberWithInt:[fbId intValue]];
@"facebookId": @(fbId) // for non pointer datatype value store in Dictionary
```

## `@property:`
[atomic, nonatomic, etc.](https://stackoverflow.com/a/15541505)

## `@synthesize:`
[@synthesize](https://stackoverflow.com/a/24890137)