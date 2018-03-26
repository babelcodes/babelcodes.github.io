---
layout: feature
language: scala
name: 'Function'
iid: Function
status: DONE
abstract: ""
code_:
  gist: 97deb7c31d1c53d0baf5de482aa09757
links_:
 - link:
    name: 'TypeScriptLang.org | Functions'
    url: https://www.typescriptlang.org/docs/handbook/functions.html
    description: ''
    type: reference
features:
 - Class
 - TypeUnit
---

* TOC
{:toc}


Functions:
- allow functionality to be treated as a method argument, or code as data.
- are also values that are assigned to variables (methods are not values)
- also have types

Functions are usually declared as an argument to another method, like what action should be taken when a service is called 
or a link is clicked on.

## First Class function

[First Class function](/functional/FirstClassFunction) can be stored, passed, and returned

For example, to define a function with a `Int` parameter named `foo` (what comes after `=>` is the body of the function):

```
// Creates a function that takes an Int as a parameter and returns Int.
// The variable type in Scala is formally declared as Int => Int
val succ = (foo: Int) => { foo + 1 }

succ(10) // Invoke the function! outputs 11
```

## Higher Order function

We can also pass functions as a parameter to other functions and methods. 

In the following example, the `adjustAndLog` method takes two parameters, an integer value, and a function that takes a 
single `Int`, and returns an `Int`:

```
def adjustAndLog(someInt: Int, adjust: Int => Int) = { 
  println(s"Adjusting $someInt")
  adjust(someInt)
}

adjustAndLog(10, (i: Int) => i + 3) // Adjust 10 adding 3 returns 13
```

A function that takes another function as argument, is called a [Higher Order function](/functional/HigherOrderFunction).
