---
layout: functional
name: 'Pure Function'
iid: PureFunction
status: DONE
abstract: "Pure functions do not rely on data outside of themselves and they do not change data that exists outside of them. They provide the same result each time that they are executed"
---

* TOC
{:toc}

## Introduction

In functional programming, __pure functions__ are the most important building blocks. Pure functions do not rely on data
 outside of themselves and they do not change data that exists outside of them. Pure functions are easy to test because 
 they will always provide the same results each time that they are executed.
 
```
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}

print("Result: \(addTwoInts(2, 3))")
```

__Pure Function is a way of programming, not an intrinsic property of languages.__ 


## Refactoring

For example, in [Scala](/Scala), the following code having __side effect__ (by charging the credit car):

```
class Cafe {
  def buyCoffee(cc: CreditCard): Coffee = {
    val cup = new Coffee()
    cc.charge(cup.price)
    cup
  }
}
``` 

can be refactored as follow (creating a `Charge` object and returning it):

```
class Cafe {
  def buyCoffee(cc: CreditCard): (Coffee, Charge) = {
    val cup = new Coffee()
    (cup, Charge(cc, cup.price))
}
```

A `Charge` is a data type we just invented containing a `CreditCard` and an amount.


## Referential transparency

A function has no observable effect on the execution of the program other than to compute a result given its inputs; we 
say that it has no __side effects__. We sometimes qualify such functions as pure functions to make this more explicit, 
but this is somewhat redundant. Unless we state otherwise, we’ll often use function to imply no side effects.

We can formalize this idea of pure functions using the concept of __referential transparency__ (RT). This is a property 
of expressions in general and not just functions. 

For the purposes of our discussion, consider an expression to be any part of a program that can be evaluated to a result—anything 
that you could type into the Scala interpreter and get an answer. For example, 2 + 3 is an expression that applies the pure 
function + to the values 2 and 3 (which are also expressions). This has no side effect. The evaluation of this expression 
results in the same value 5 every time. In fact, if we saw 2 + 3 in a program we could simply replace it with the value 5 
and it wouldn’t change a thing about the meaning of our program.

This is all it means for an expression to be referentially transparent—in any program, the expression can be replaced by 
its result without changing the meaning of the program. And we say that a function is pure if calling it with RT arguments 
is also RT.

### Referential transparency and purity

> An expression `e` is __referentially transparent__ if, for all programs `p`, all occurrences of `e` in `p` can be replaced 
> by the result of evaluating `e` without affecting the meaning of `p`. 
>
> A function `f` is __pure__ if the expression `f(x)` is referentially transparent for all referentially transparent `x`.


### Substitution model & Equational reasoning

This property of pure functions is called referential transparency and makes it possible to conduct __equational reasoning__ 
on the code (computation proceeds by substituting equals for equals).

_Referential transparency_ forces the invariant that everything a function does is represented by the value that it returns, 
according to the result type of the function. This constraint enables a simple and natural mode of reasoning about program 
evaluation called the __substitution model__. When expressions are referentially transparent, we can imagine that computation 
proceeds much like we’d solve an algebraic equation. We fully expand every part of an expression, replacing all variables 
with their referents, and then reduce it to its simplest form. 

At each step we replace a term with an equivalent one; computation proceeds by substituting equals for equals. In other 
words, RT enables equational reasoning about programs.

The _substitution model_ is simple to reason about since effects of evaluation are purely local (they affect only the 
expression being evaluated) and we need not mentally simulate sequences of state updates to understand a block of code. 
Understanding requires only local reasoning.

## Why?

Formalizing the notion of _purity_ this way gives insight into why functional programs are often more modular. Modular 
programs consist of components that can be understood and reused independently of the whole, such that the meaning of 
the whole depends only on the meaning of the components and the rules governing their composition; that is, they are 
composable.

A pure function is modular and composable because it separates:
* the logic of the computation itself 
* from “what to do with the result / output”  (simply computed and returned)
* and “how to obtain the input” (obtained in exactly one way: via the argument(s) to the function)

It’s a black box.

Pure functions can be executed on different threads or cores without any mechanisms to handle multithreading and multiprocessing. 
This is a very important benefit of functional programming over OOP as multicore programming mechanisms are very complex 
to handle in OOP. Also, programming for multicore computers is becoming more important day by day because hardware engineers 
have finally hit the speed limit of light. Computer clocks will not be getting faster in the near future so, in order to 
have more cycles per second, hardware engineers are adding more processors to chips. There seems no end to how many processors 
we will have in our computers. A higher number of processors to be used for a program means a more complex multithreading 
and multicore mechanism to handle.

Functional programming eliminates the need for a complex multicore programming mechanism, and as pure functions are not 
dependent on any instances or data outside of themselves, it is easy to change them without changing other parts.
