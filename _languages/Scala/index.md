---
layout: language
type: language
name: 'Scala'
iid: scala
status: DOING
icon: /resources/images/languages/Scala/scala.png
abstract: ""
links_:
 - link:
    name: 'The Swift Programming Language: A Swift Tour'
    url: https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/GuidedTour.html#//apple_ref/doc/uid/TP40014097-CH2-ID1
    description: ' - Apple Developer'
    type: reference
features:
  TypeSafety: true
  TypeInference: true
  Immutability: true
  PureFunction: true
  FirstClassFunction: true
  HigherOrderFunction: true
  PatternMatching: true
---

* TOC
{:toc}

## What is it?

Scala is a general-purpose programming language designed to express common programming patterns in a concise, elegant, and 
[type-safe way](/functional/TypeSafety). It smoothly integrates features of object-oriented and functional programming languages, 
enabling programmers to be more productive. Scala is an acronym for “Scalable Language”. This means that Scala grows with you.

An important aspect of Scala is that it runs inside the JVM. That means it can leverage existing Java Libraries and libraries 
written in Scala can be called from [Java](/Java/7).

See the importance of __Referential transparency and purity__ in the [Pure Function](/functional/PureFunction) page.

## Main topics

* [Constants](Constant) / [Immutability](/functional/immutability) and [Variables](Variable), the [Unit type](Unit)
* [Classes](Class) and [Traits](Trait)
* Higher Order [functions](Function)
* [Collections](Collections)


Scala is fully expression-oriented:

<pre><code>val second = { 
  val tmp = 2 * 5
  tmp + 88
}
</code></pre>

or:

<pre><code>val second = 43
val displayFlag = if (second % 2 == 0) {
  "Second is Even" }
else {
  "Second is Odd"
}
</code></pre>

Or, in shorthand notation, this could be expressed as:

<pre><code>val displayFlag = if (second%2 == 0) "Second is Even"
else
"Second is Odd"
</code></pre>


## Some useful collections and streams utilities

`List.fill(n)(x)` creates a List with n copies of x:
```
val purchases: List[(Coffee, Charge)] = List.fill(n)(buyCoffee(cc))
```

`unzip` splits a list of pairs into a pair of lists:
```
val (coffees, charges) = purchases.unzip
```

`charges.reduce` reduces the entire list of charges to a single charge:
```
charges.reduce((c1,c2) => c1 + c2))
```


With a `Charge` object having the following content:

```
case class Charge(cc: CreditCard, amount: Double) {
  def combine(other: Charge): Charge = 
    if (cc == other.cc)
      Charge(cc, amount + other.amount)
    else
      throw new Exception("Can't combine charges to different cards")
  }
}
```

we can write (The `_.cc` and `_ combine _` are syntax for anonymous functions) to take a list of charges, group them by 
the credit card used, and then combine them into a single charge per card:

```
charges.groupBy(_.cc).values.map(_.reduce(_ combine _)).toList
```