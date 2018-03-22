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
  FirstClassFunction: '?'
  PatternMatching: true
  HigherOrderFunction: true
---

* TOC
{:toc}

## What is it?

Scala is a general-purpose programming language designed to express common programming patterns in a concise, elegant, and 
[type-safe way](/functional/TypeSafety). It smoothly integrates features of object-oriented and functional programming languages, 
enabling programmers to be more productive. Scala is an acronym for “Scalable Language”. This means that Scala grows with you.

An important aspect of Scala is that it runs inside the JVM. That means it can leverage existing Java Libraries and libraries 
written in Scala can be called from [Java](/Java/7).


## Main topics

* [Constants](/Constant) / [Immutability](/functional/immutability) and [Variables](/Variable)
* [Classes](Class) and [Traits](Trait)
* Higher Order [functions](Function)

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
