---
layout: feature
language: typescript
name: 'Class'
iid: Class
status: DOING
abstract: ""
code:
  gist: a084aead5a3acb71c8340b7b6c7ba86e 
links:
 - link_:
    name: 'TypeScriptLang.org | Basic Types'
    url: https://www.typescriptlang.org/docs/handbook/basic-types.html
    description: ''
    type: reference
features:
- Constructor
- Properties
- Visibility 
- Readonly
- Methods
- Extends 
- Abstract 
- Accessors
- Static
---

* TOC
{:toc}

## Definition

```
class Greeter {
}

let greeter = new Greeter();
```

## Constructor

```
class Greeter {
    constructor(message: string) {
    }
}
```

## Properties 

```
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
}

let greeter = new Greeter("world");
console.log(greeter.greeting);
```

## Methods 

- `this`
- `private`

```
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = "Hello" + message;
    }
    sayHello(): string {
        return this.greeting = "Hello" + message;
    }
}

let greeter = new Greeter("world");
console.log(greeter.sayHello());
```

## Visibility 

- `public` / `protected` / `private` constructor parameters
- Compile time constraint. Everything public at runtime 


## Readonly variable 

You can make properties readonly by using the `readonly` keyword. Readonly properties must be initialized at their declaration or in the constructor.

Compile time.

```
class Octopus {
    readonly name: string;
    readonly numberOfLegs: number = 8;
    constructor (theName: string) {
        this.name = theName;
    }
}
let dad = new Octopus("Man with the 8 strong legs");
dad.name = "Man with the 3-piece suit"; // error! name is readonly.
```


## Inheritance / Extends
 
- inherit constructors

```
class Person {
}

class Employee extends Person {
}
```

 
## Abstract 

Abstract classes are base classes from which other classes may be derived. They may not be instantiated directly. Unlike 
an interface, an abstract class may contain implementation details for its members. The abstract keyword is used to define 
abstract classes as well as abstract methods within an abstract class.

```
abstract class Animal {
    abstract makeSound(): void;
    move(): void {
        console.log("roaming the earth...");
    }
}

class Cat extends Animal {

    makeSound(): void {
    }

}
```

## Accessors: getters & setters
 
- property or method getter

```
class Employee {
    fullName: string;
}

let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) {
    console.log(employee.fullName);
}
```

## Static Properties

```
class Grid {
    static origin = {x: 0, y: 0};
    calculateDistanceFromOrigin(point: {x: number; y: number;}) {
        let xDist = (point.x - Grid.origin.x);
        let yDist = (point.y - Grid.origin.y);
        return Math.sqrt(xDist * xDist + yDist * yDist) / this.scale;
    }
    constructor (public scale: number) { }
}

let grid1 = new Grid(1.0);  // 1x scale
let grid2 = new Grid(5.0);  // 5x scale

console.log(grid1.calculateDistanceFromOrigin({x: 10, y: 10}));
console.log(grid2.calculateDistanceFromOrigin({x: 10, y: 10}));
```