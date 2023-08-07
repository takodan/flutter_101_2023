# Dart Programming Tutorial - Full Course
1. dart is a statically type programming language
2. dart is a compiled programming language
    1. AOT, ahead of time: compile at build.
    2. JIT, just in time: compile at runtime.


## Starts
```dart
void main() {
    // "void" means return nothing
    var firstName = 'Dan'; // type inference推論
    const middleName = 'what'; // constant variable
    String lastName = 'Chang'; // type defined
}
```


## input, output, print
```dart
import 'dart:io';
void main() {
    stdout.writeln('Your name: ');
    String name= stdin.readLineSync();
    print('My name is $name'); // string interpolation
}
```


## comment
```dart
// In-line
/*
Block
*/
/// Documentation
```


## data type
1. ~~Strongly~~Statically type language: the type is known at compile time.
2. Dynamic type language: the type is known at run time.
```dart
void main() {
    int amount = 100;
    double dAmount = 100.11;

    String name = 'Dan';
    String s = "double quotes work";
    String rawString = r'this is a row \n string.';

    bool isTrue = true;

    dynamic dyVariable = 100;
    dyVariable = 'Wah';

    print(dyVariable.runtimeType) // string
}
```
### NOTE: static and dynamic
stack overflow. [What is the difference between statically typed and dynamically typed languages?](https://stackoverflow.com/questions/1517582/what-is-the-difference-between-statically-typed-and-dynamically-typed-languages)  
stack overflow. [What is the difference between a strongly typed language and a statically typed language?](https://stackoverflow.com/questions/2690544/what-is-the-difference-between-a-strongly-typed-language-and-a-statically-typed)  


## Null Aware Operators: (?.), (??), and (??=) 
```dart
// (object?.): if (object != null) then run
void main() {
    dynamic n1; // dynamic is nullable
    int? n2 = 100; // add (?) to the type to indicate that the variable can be null
  
    n2 = n1?.number; // (n1) is null, it won't run (.number). assign n1 to (n2), that is null  

    print(n2); // null
}
```
```dart
// (a ?? b): if (a == null), run (b)
void main() {
    dynamic n1;
    int? n2 = 100;

    n2 = n1 ?? 200; // (n1) is null, so assign (200) to (n2)

    print(n2); // 200
}
```
```dart
// (a ??= b): if (a == null), assign (b) to (a)
void main() {
    dynamic n1;
    n1 ??= 100; // (n1) is null, so assign (100) to (n1)

    print(n1); // 100
}
```
### NOTE: cheat sheet about null in Dart
Dart. [Understanding null safety](https://dart.dev/null-safety/understanding-null-safety)  
Dart. [Dart cheatsheet codelab](https://dart.dev/codelabs/dart-cheatsheet#nullable-variables)  

## Conditional (Ternary) Operator: (?)
```dart
String ternaryOperator(bool foo){
    return foo ? 'foo is TRUE return this' : 'foo is FALSE return this'
}
void main() {
    print(ternaryOperator(true));
}
```


## Conditional Statement
```dart
if(){} else if(){} else{}
```
or you can use (switch)
```dart
void main() {
    int number = 10;

    switch(number) {
        case 10:
            print(10);
            break;
        case 20:
            print(20);
            break;
        default:
            print('default');
    }
    // case((number) == 10), print 10
}
```


## Loop
```dart
void main(){
    var numbers = [0, 1, 2];
    // for loop
    for(var i=0 ; i<numbers.length ; i++) {
        print(i);
    }
    for(var n in numbers) {
        print(n);
    }

    // forEach loop, avoid
    numbers.forEach( (var n) => print(n));

    // while loop
    int n = 0;
    while(n<3){
        print(n);
        n++;
    }
    do{
        print(n);
        n++;
    }while(n<2);

    // break and continue also work
}
```
### NOTE: AVOID using forEach with a function literal
Dart.[avoid_function_literals_in_foreach_calls](https://dart.dev/tools/linter-rules/avoid_function_literals_in_foreach_calls)

## List (Array)
```dart
var names1 = <String>['string1', 'string2'];
List <String> names2 = ['string1', 'string2'];
// <String> means elements type should be String

// (const) make this List constant
List <String> names3 = const ['string1', 'string2'];

// use Spread Operator (...) to deep copy a List
var names4 = [...name3];

// List methods
names4.length
names4.add('string3')
names4.addAll(names1)
names4.insert(3, "9000") // (position, item)
names4.remove("9000") // (item)
names4.removeAt(0) // (position)
```

## Set
A collection of objects in which each object can occur only once.
```dart
var names1 = <String>{"a", "b"};
Set <String> names2 = {};
```

## Map (Dictionary)
```dart
var names1 = <String,String>{"a":"b", "c":"d"};
Map<String,String> names2 = {};
```

## Function
start with return value type
```dart
void funName1(var number) {
    // no return
    print(number);
}
dynamic funName2(var number) {
    // return dynamic variable
    return number * number;
}

// Arrow Function
dynamic sameAsFunName2(var number) => number * number; // return number * number

// Anonymous Function
(number){print(number)};
(var number) => print(number); // return null

// more parameter
// positional and optional parameters
dynamic sum1(var n1, [var n2=2]){
    return n1 + n2;
}
// named parameters are also optional
dynamic sum2(var n1, {var n2=4}){
    return n1 + n2;
}
void main(){
    print(sum1(1)); // 1 + 2 = 3
    print(sum1(1, 3)); // 1 + 3 = 4
    print(sum2(2)); // 2 + 4 = 6
    print(sum2(2, n2:5)); // 2 + 5 = 7
}
```
### NOTE: Named, Optional, and positional parameters
Dart. [Parameters](https://dart.dev/language/functions#parameters)


## Class
```dart
class Person {
    String? name;
    int? age;

    // constructor
    //Person(String name, [int? age]) {
    //    this.name = name;
    //    this.age = age ?? 0;
    //}

    // initializing formals
    Person( this.name, [this.age = 1]);

    // name constructor
    Person.guest() {
        name = 'Guest';
        age = 0;
    }

    //method
    void showOutput(){
        print(name);
        print(age);
    }
}
void main() {
    Person person1 = Person('Dan');
    Person person2 = Person.guest();

    person1.showOutput(); // Dan 1
    person2.showOutput(); // Guest 0
}
```
### NOTE: DO use initializing formals when possible.
Dart. [prefer_initializing_formals](https://dart.dev/tools/linter-rules/prefer_initializing_formals)  


## Late, final, and const. static
```dart
class Person {
    // (late): initialized after its declaration
    // (final): a variable can be set only once
    late final String name;

    // (static): class-wide variables or methods
    // (const): compile-time constants
    // Only static fields can be declared as const.
    static const int age =10;
}
void main() {
    // you can use (const) without static in a function
    const int number = 100;

    Person person1 = Person();
    person1.name = 'Dan';
    print(person1.name);
    print(Person.age);

}
```
### NOTE: Late, final, and const.
Dart. [Variables](https://dart.dev/language/variables#late-variables)  
Dart. [Classes](https://dart.dev/language/classes#class-variables-and-methods)


## Inheritance and Override
```dart
class Person {
    String? name;
    int? age;
  
    Person( this.name, [this.age = 1]){
      print('This class inherit Person');
    }

    void showOutput(){
        print(name);
        print(age);
    }
}

class Employee extends Person {
    int? id;
    
    // inherit superclass' constructor
    Employee(String name, int age, this.id) : super(name, age);
    
    // (@override) superclass' method with same name
    @override
    void showOutput(){
        // inherit superclass' method
        super.showOutput();
        print(id);
    }
}
void main() {
    var person1 = Employee('Dan',28,7);

    print('-----');
    person1.showOutput();
}
// output:

// This class inherit Person
// -----
// Dan
// 28
// 7
```

### Getter and Setter
```dart
class Person {
    String? name;
    Person(this.name);

    // Getter
    String? get getName => name;
    // as same as
    // String? getName(){
	// return name;
    // }

    // Setter
    set setName(String newString) => name = newString;
}

void main() {
    var person1 = Person('Dan');

    print(person1.getName); // Dan
    person1.setName = 'Dummy';
    print(person1.getName); // Dummy
}
```
### NOTE: private, getter, setter, and static
2021 iThome 鐵人賽Todd. [Day 06 | Dart基本介紹 - private & static](https://ithelp.ithome.com.tw/articles/10265940)  


## Exception Handling
```dart
int greaterThanZero(int val){
    if (val <= 0) {
        throw Exception('Value is not greater than zero!');
    }
    return val;
}
void verifyTheValue(var val){
    dynamic verification = 'fail';
    try{
        verification = greaterThanZero(val);
    }
    catch(exception){
        print(exception);
    }
    finally{
        print('verified: $verification');
    }
}
void main() {
    verifyTheValue(0);
    // Exception: Value is not greater than zero!
    // verified: fail
    verifyTheValue(10);
    // verified: 10
}
```

