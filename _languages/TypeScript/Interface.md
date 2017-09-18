---
layout: feature
language: typescript
name: 'Interface'
iid: Interface
status: DONE
abstract: ""
code:
  gist: 54e9f8c7a70fd381b327cc15b3855e5a 
links:
 - link_:
    name: 'TypeScriptLang.org | Interfaces'
    url: https://www.typescriptlang.org/docs/handbook/interfaces.html
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


## Introduction

One of TypeScript’s core principles is that type-checking focuses on the shape that values have. This is sometimes called 
&laquo; duck typing &raquo; or &laquo; structural subtyping &raquo;. 
In [TypeScript](/TypeScript), __interfaces__ fill the role of naming these types, and are a powerful way of defining contracts 
within your code as well as contracts with code outside of your project.

One of the most common uses of interfaces in common languages is to explicitly enforcing that a class meets a particular contract.

It is possible to describe both properties and methods in an _interface_ that are implemented in the class:

```
   interface ClockInterface {
       currentTime: Date;       // property
       setTime(d: Date);        // method
   }
   
   class Clock implements ClockInterface {
       currentTime: Date;
       setTime(d: Date) { this.currentTime = d; }
       constructor(h: number, m: number) { }
   }
```

In [TypeScript](/TypeScript) an __interface__ can also be used to describe an object:

```
    interface LabelledValue {
        label: string;
    }
    let myObj :LabelledValue = { label: "Size 10 Object" };           // OK
    let myObj :LabelledValue = { label: "Size 10 Object", size: 33 }; // NOK
```

It can be used to describe a function __type__:

```
    interface SearchFunc {
        (source: string, subString: string): boolean;
    }
    let mySearch: SearchFunc = function(source: string, subString: string) {
        return source.search(subString) > -1;
    }
```

It can be used to describe a constructor type:

```
    interface ClockConstructor {
        new (hour: number, minute: number): ClockInterface;
    }
```

And it is possible to combine those types in a same interface to describe a [hybrid types](#hybrid-types).

## Definition

```
    interface LabelledValue {
        label: string;
    }
    
    function printLabel(labelledObj: LabelledValue) {
        console.log(labelledObj.label);
    }
    
    let myObj = {size: 10, label: "Size 10 Object"};
    printLabel(myObj);
```

We define here an _interface_ with only [properties](/TypeScript/Class#properties). 

Notice we didn’t have to explicitly say that the object we pass to `printLabel` implements this interface like we might have 
to in other languages.


## Optional Properties with `?`

Not all properties of an interface may be required.

```
    interface SquareConfig {
        color?: string;
        width?: number;
    }
     
    function createSquare(config: SquareConfig): {color: string; area: number} {
        let newSquare = {color: "white", area: 100};
        if (config.color) {
            newSquare.color = config.color;
        }
        if (config.width) {
            newSquare.area = config.width * config.width;
        }
        return newSquare;
    }
     
    let mySquare = createSquare({color: "black"});
```

## Readonly properties

```
    interface Point {
        readonly x: number;
        readonly y: number;
    }
     
    let p1: Point = { x: 10, y: 20 };
    p1.x = 5; // error!
```

[TypeScript](/TypeScript) comes with a `ReadonlyArray<T>` type that is the same as `Array<T>` with all mutating methods removed:

```
    let a: number[] = [1, 2, 3, 4];
    let ro: ReadonlyArray<number> = a;
    ro[0] = 12;         // error!
    ro.push(5);         // error!
    ro.length = 100;    // error!
    a = ro;             // error!
    a = ro as number[];
```

### readonly vs const

Variables use `const` whereas properties use `readonly`.


## Excess Property Checks

An error occurs an object is associated to an `Interface` with some additional properties:

```
    interface SquareConfig {
        color?: string;
        width?: number;
    }
    
    let mySquare1 :SquareConfig = { colour: "red", width: 100 }; // error: 'colour' (vs 'color') not expected in type 'SquareConfig'
    let mySquare2 :SquareConfig = { width: 100, opacity: 0.5 } as SquareConfig; // use a type assertion
```

A better approach might be to add a string index signature:

```
    interface SquareConfig {
        color?              : string;
        width?              : number;
        [propName: string]  : any;
    }
```

Another way is to assign to another variable:

```
    let squareOptions = { colour: "red", width: 100 };
    let mySquare = createSquare(squareOptions);
```

## Function Types

_Interfaces_ are also capable of describing function __types__ (vs describing function). 
This is like a function declaration with only the parameter list and return type given

```
    interface SearchFunc {
        (source: string, subString: string): boolean;
    }
```

It can then be used as any other _interfaces_:

```
    let mySearch: SearchFunc;
    mySearch = function(source: string, subString: string) {
        let result = source.search(subString);
        return result > -1;
    }
```

The names of the parameters do not need to match.

See also the [Constructor Types](#constructor-types) section below.


## Indexable Types

To describe types that we can "index into" like `a[10]` or `ageMap["daniel"]`. 

Indexable types have an index signature that describes the types we can use to index into the object, along with the corresponding 
return types when indexing:

```
interface StringArray {
    [index: number]: string;
}

let myArray: StringArray;
myArray = ["Bob", "Fred"];

let myStr: string = myArray[0];
```

Above, we have a `StringArray` _interface_ that has an __index signature__. This index signature states that when a 
`StringArray` is indexed with a `number`, it will return a `string`.

There are two types of supported index signatures: `string` and `number`. It is possible to support both types of indexers, 
but the type returned from a numeric indexer must be a subtype of the type returned from the string indexer. 


### As a dictionary... with all elements having same type

While string index signatures are a powerful way to describe the &laquo; dictionary &raquo; pattern, they also enforce that 
all properties match their return type. This is because a string index declares that `obj.property` is also available as 
`obj["property"]`. 

In the following example, name’s type does not match the string index’s type, and the type-checker gives an error:

```
    interface NumberDictionary {
        [index: string]: number;
        length         : number;     // ok, length is a number
        name           : string;     // error, the type of 'name' is not a subtype of the indexer
    }
```

### Readonly

Finally, you can make index signatures readonly in order to prevent assignment to their indices:

```
    interface ReadonlyStringArray {
        readonly [index: number]: string;
    }
    let myArray: ReadonlyStringArray = ["Alice", "Bob"];
    myArray[2] = "Mallory";          // error!
```


## Class Types

### Implementing an interface
   
One of the most common uses of interfaces in languages like C# and Java, that of explicitly enforcing that a class meets 
a particular contract, is also possible in TypeScript.

It is possible to describe both properties and methods in an interface that are implemented in the class:

```
   interface ClockInterface {
       currentTime: Date;       // property
       setTime(d: Date);        // method
   }
   
   class Clock implements ClockInterface {
       currentTime: Date;
       setTime(d: Date) {
           this.currentTime = d;
       }
       constructor(h: number, m: number) { }
   }
```

The modifiers are prohibited (`public`, `private`): everything is public in an _interface_.


## Constructor Types

An _interface_ can also has a construct signature:

```
    interface ClockConstructor {
        new (hour: number, minute: number): ClockInterface;
    }
```

### static vs instance sides

When a class implements an interface, only the instance side of the class is checked. 
Since the constructor sits in the static side, it is not included in this check.

__A class can not implements a constructor interface.__

```
    interface ClockConstructor {
        new (hour: number, minute: number): ClockInterface;
    }
    interface ClockInterface {
        tick();
    }
    
    function createClock(ctor: ClockConstructor, hour: number, minute: number): ClockInterface {
        return new ctor(hour, minute);
    }
    
    class DigitalClock implements ClockInterface {
        constructor(h: number, m: number) { }
        tick() {
            console.log("beep beep");
        }
    }
    class AnalogClock implements ClockInterface {
        constructor(h: number, m: number) { }
        tick() {
            console.log("tick tock");
        }
    }
    
    let digital = createClock(DigitalClock, 12, 17);
    let analog = createClock(AnalogClock, 7, 32);
```

## Extending Interfaces

Like classes, interfaces can extend each other and can extend multiple interfaces.

```
    interface Shape {
        color: string;
    }
    
    interface PenStroke {
        penWidth: number;
    }
    
    interface Square extends Shape, PenStroke {
        sideLength: number;
    }
    
    let square = <Square>{};
    square.color = "blue";
    square.sideLength = 10;
    square.penWidth = 5.0;
```

## Hybrid Types

Through interfaces it is possible to describe an object that works as a combination of:
- properties
- methods
- function types

```
    interface Counter {
        (start: number): string;    // Function type
        interval: number;           // Property
        reset(): void;              // Method
    }
    
    function getCounter(): Counter {
        let counter = <Counter>function (start: number) { };
        counter.interval = 123;
        counter.reset = function () { };
        return counter;
    }
    
    let c = getCounter();
    c(10);
    c.reset();
    c.interval = 5.0;
```

When interacting with 3rd-party JavaScript, you may need to use patterns like the above to fully describe the shape of 
the type.


## Interfaces Extending Classes

When an interface type extends a class type it inherits the members of the class but not their implementations. 

Interfaces inherit even the private and protected members of a base class. This means that when you create an interface 
that extends a class with private or protected members, that interface type can only be implemented by that class or a 
subclass of it.
   
This is useful when you have a large inheritance hierarchy, but want to specify that your code works with only subclasses 
that have certain properties. The subclasses don’t have to be related besides inheriting from the base class. 
For example:
   
```
    class Control {
        private state: any;
    }
    
    interface SelectableControl extends Control {
        select(): void;
    }
    
    class Button extends Control implements SelectableControl {
        select() { }
    }
    
    class TextBox extends Control {
    
    }
    
    // Error: Property 'state' is missing in type 'Image'.
    class Image implements SelectableControl {
        select() { }
    }
    
    class Location {
    }
```
