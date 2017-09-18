---
layout: feature
language: typescript
name: 'Type'
iid: Type
status: DOING
abstract: ""
code:
  gist: d9d2a3325e50589004867c5bd23d68f6
links:
 - link:
    name: 'TypeScriptLang.org | Basic Types'
    url: https://www.typescriptlang.org/docs/handbook/basic-types.html
    description: ''
    type: reference
features:
 - 'Loose typing' 
 - 'Post-fix typing'
 - 'Type aliasing'
 - 'Type Union'
 - 'Type Intersection'
 - 'this type'
 - 'Discriminated type'
---

* TOC
{:toc}

One of TypeScript’s core principles is that type-checking focuses on the shape that values have. This is sometimes called “duck typing” or “structural subtyping”.

## Basic types

{% gist d9d2a3325e50589004867c5bd23d68f6 %}

## Loose typing

Can be dynamic or static

## Post-fix typing

For a variable:

```
let isDone :boolean = true; // ":boolean" is optional
```

Or a function:

```
function add(x: number, y: number): number {
    return x + y;
}
```

## Aliasing 

enum like:

```
type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
function getName(n: NameOrResolver): Name {
    if (typeof n === "string") {
        return n;
    }
    else {
        return n();
    }
}
```

## Union

Using `|`:

```
type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
function getName(n: NameOrResolver): Name {
    if (typeof n === "string") {
        return n;
    }
    else {
        return n();
    }
}

```

## Intersection

Using `&`:

```
function extend<T, U>(first: T, second: U): T & U {
    let result = <T & U>{};
    for (let id in first) {
        (<any>result)[id] = (<any>first)[id];
    }
    for (let id in second) {
        if (!result.hasOwnProperty(id)) {
            (<any>result)[id] = (<any>second)[id];
        }
    }
    return result;
}

class Person {
    constructor(public name: string) { }
}
interface Loggable {
    log(): void;
}
class ConsoleLogger implements Loggable {
    log() {
        // ...
    }
}
var jim = extend(new Person("Jim"), new ConsoleLogger());
var n = jim.name;
jim.log();
```

## `this`

TODO

## Discriminated type

TODO
