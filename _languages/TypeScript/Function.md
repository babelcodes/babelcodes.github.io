---
layout: feature
language: typescript
name: 'Function'
iid: Function
status: DONE
abstract: "Functions are the fundamental building block of any applications in JavaScript. They’re how you build up layers of abstraction, mimicking classes, information hiding, and modules. In TypeScript, while there are classes, namespaces, and modules, functions still play the key role in describing how to do things. TypeScript also adds some new capabilities to the standard JavaScript functions to make them easier to work with."
code:
  gist: 97deb7c31d1c53d0baf5de482aa09757
links:
 - link:
    name: 'TypeScriptLang.org | Functions'
    url: https://www.typescriptlang.org/docs/handbook/functions.html
    description: ''
    type: reference
features:
 - 'this' 
---

* TOC
{:toc}


Functions are the fundamental building block of any applications in JavaScript. They’re how you build up layers of abstraction, 
mimicking classes, information hiding, and modules. In TypeScript, while there are classes, namespaces, and modules, functions 
still play the key role in describing how to do things. TypeScript also adds some new capabilities to the standard JavaScript 
functions to make them easier to work with.


## Definition

### As in JavaScript

TypeScript functions can be created both:

- as a named function or 
- as an anonymous function

```
// Named function
function add(x, y) { return x + y; }

// Anonymous function
let myAdd = function(x, y) { return x + y; };
```

Functions can refer to variables outside of the function body. When they do so, they’re said to __capture__ these variables:

```
let z = 100;

function addToZ(x, y) {
    return x + y + z;
}
```

But that fail the __pure function__ concept.

##Function Types

### Typing the function

We can add types to each of the parameters and then to the function itself to add a return type. 
TypeScript can figure the return type out by looking at the return statements, so we can also optionally leave this off in many cases.

```
function add(x: number, y: number): number {
    return x + y;
}

let myAdd = function(x: number, y: number): number { return x + y; };
```

### Writing the function type

Let’s write the full type of the function out by looking at the each piece of the function type:

```
let myAdd: (something: number, somethingElse: number) => number =
    function(x: number, y: number): number { return x + y; };
```

### Inferring the types or Contextual typing

```
// myAdd has the full function type
let myAdd = function(x: number, y: number): number { return  x + y; };

// The parameters 'x' and 'y' have the type number
let myAdd: (baseValue: number, increment: number) => number = function(x, y) { return x + y; };
```


## Optional and Default Parameters

### Required (by default)

While in JavaScript, every parameter is optional, in TypeScript, every parameter is assumed to be required by the function. This doesn’t mean that it can’t be given `null` or `undefined`.

In short, the number of arguments given to a function has to match the number of parameters the function expects.

```
function buildName(firstName: string, lastName: string) {
    return firstName + " " + lastName;
}

let result1 = buildName("Bob");                  // ERROR, too few parameters
let result2 = buildName("Bob", "Adams", "Sr.");  // ERROR, too many parameters
let result3 = buildName("Bob", "Adams");         // ah, just right
```

### Optional

To do as JavaScript end define an optional parameter with `undefined` as default value we use a `?` at the end of the parameter name:

```
function buildName(firstName: string, lastName?: string) {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName;
}

let result1 = buildName("Bob");                  // works correctly now
let result2 = buildName("Bob", "Adams", "Sr.");  // ERROR, too many parameters
let result3 = buildName("Bob", "Adams");         // ah, just right
```

Any optional parameters must follow required parameters.

### Default-initialized parameters

```
function buildName(firstName: string, lastName = "Smith") {
    return firstName + " " + lastName;
}

let result1 = buildName("Bob");                  // works correctly now, returns "Bob Smith"
let result2 = buildName("Bob", undefined);       // still works, also returns "Bob Smith"
let result3 = buildName("Bob", "Adams", "Sr.");  // error, too many parameters
let result4 = buildName("Bob", "Adams");         // ah, just right
```

Default-initialized parameters that come after all required parameters are treated as optional, and just like optional parameters, 
can be omitted when calling their respective function. 

This means optional parameters and trailing default parameters will share commonality in their types, so both:

```
function buildName(firstName: string, lastName?: string) {
    // ...
}
```

and 

```
function buildName(firstName: string, lastName = "Smith") {
    // ...
}
```

share the same type:

```
(firstName: string, lastName?: string) => string
```

The default value of `lastName` disappears in the type, only leaving behind the fact that the parameter is optional.

Unlike plain optional parameters, default-initialized parameters don’t need to occur after required parameters. 
If a default-initialized parameter comes before a required parameter, users need to explicitly pass `undefined` to get the 
default initialized value.

```
function buildName(firstName = "Will", lastName: string) {
    return firstName + " " + lastName;
}

let result1 = buildName("Bob");                  // error, too few parameters
let result2 = buildName("Bob", "Adams", "Sr.");  // error, too many parameters
let result3 = buildName("Bob", "Adams");         // okay and returns "Bob Adams"
let result4 = buildName(undefined, "Adams");     // okay and returns "Will Adams"
```

## Rest Parameters

Sometimes, you want to work with multiple parameters as a group, or you may not know how many parameters a function will 
ultimately take. In JavaScript, you can work with the arguments directly using the `arguments` variable that is visible inside 
every function body.

In TypeScript, you can gather these arguments together into a variable:

```
function buildName(firstName: string, ...restOfName: string[]) {
    return firstName + " " + restOfName.join(" ");
}

let employeeName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie");
```

Rest parameters are treated as a boundless number of optional parameters.

The ellipsis "`...`" is also used in the type of the function with rest parameters:

```
function buildName(firstName: string, ...restOfName: string[]) {
    return firstName + " " + restOfName.join(" ");
}

let buildNameFun: (fname: string, ...rest: string[]) => string = buildName;
```


## this

See [this](this)


## Overloads

JavaScript is inherently a very dynamic language. It’s not uncommon for a single JavaScript function to return different 
types of objects based on the shape of the arguments passed in.

```
let suits = ["hearts", "spades", "clubs", "diamonds"];

function pickCard(x): any {
    // Check to see if we're working with an object/array
    // if so, they gave us the deck and we'll pick the card
    if (typeof x == "object") {
        let pickedCard = Math.floor(Math.random() * x.length);
        return pickedCard;
    }
    // Otherwise just let them pick the card
    else if (typeof x == "number") {
        let pickedSuit = Math.floor(x / 13);
        return { suit: suits[pickedSuit], card: x % 13 };
    }
}

let myDeck = [{ suit: "diamonds", card: 2 }, { suit: "spades", card: 10 }, { suit: "hearts", card: 4 }];
let pickedCard1 = myDeck[pickCard(myDeck)];
alert("card: " + pickedCard1.card + " of " + pickedCard1.suit);

let pickedCard2 = pickCard(15);
alert("card: " + pickedCard2.card + " of " + pickedCard2.suit);
```

Here the `pickCard` function will return two different things based on what the user has passed in.

But how do we describe this to the type system?

The answer is to supply multiple function types for the same function as a list of overloads.

```
let suits = ["hearts", "spades", "clubs", "diamonds"];

function pickCard(x: {suit: string; card: number; }[]): number; // Overloads #1
function pickCard(x: number): {suit: string; card: number; };   // Overloads #2
function pickCard(x): any {
    // Check to see if we're working with an object/array
    // if so, they gave us the deck and we'll pick the card
    if (typeof x == "object") {
        let pickedCard = Math.floor(Math.random() * x.length);
        return pickedCard;
    }
    // Otherwise just let them pick the card
    else if (typeof x == "number") {
        let pickedSuit = Math.floor(x / 13);
        return { suit: suits[pickedSuit], card: x % 13 };
    }
}

let myDeck = [{ suit: "diamonds", card: 2 }, { suit: "spades", card: 10 }, { suit: "hearts", card: 4 }];
let pickedCard1 = myDeck[pickCard(myDeck)];
alert("card: " + pickedCard1.card + " of " + pickedCard1.suit);

let pickedCard2 = pickCard(15);
alert("card: " + pickedCard2.card + " of " + pickedCard2.suit);
```

With this change, the overloads now give us type-checked calls to the `pickCard` function.

The compiler follows a similar process to the underlying JavaScript: it looks at the overload list. 
For this reason, its customary to order overloads from most specific to least specific.

Note that the function `pickCard(x): any` piece is not part of the overload list, so it only has two overloads: 
1. one that takes an object 
1. and one that takes a number. 

Calling `pickCard` with any other parameter types would cause an error.

