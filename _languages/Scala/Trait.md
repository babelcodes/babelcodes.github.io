---
layout: feature
name: 'Trait'
iid: Trait
status: DONE
language: scala
abstract: ""
code_:
  gist: ac6040f564565c68b72054edf60e05b2
  iswift: 5erSyB
links_:
 - link:
    name: 'The Swift Programming Language: A Swift Tour'
    url: https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/GuidedTour.html#//apple_ref/doc/uid/TP40014097-CH2-ID1
    description: ' - Apple Developer'
    type: reference
features:
 - Class
 - Function
features_:
 - AccessControl
 - ClassMethod
 - Closure
 - Enumeration
 - Extension
 - Protocol
 - Structure
 - TypeMethod
 - Subscripts
 - Properties
---

* TOC
{:toc}

Traits can be viewed as an interface that provides a default implementation of some of the methods ([Java 8](/Java/8) added 
something similar with default methods on interfaces).

Traits:
- may not have constructor parameters
- are not instantiated directly like a class
- can be used similarly to an abstract class

<pre><code>// Declaring a trait with an abstract method 
trait Greetings {
  def sayHello: String 
}

class JapaneseGreetings extends Greetings { 
  override def sayHello: String = "konnichiwa"
}
</code></pre>


Traits can also be used to provide methods and variables that are mixed into a class instead of being extended:

<pre><code>trait DefaultGreetings {
  def defaultHello = "Hello" 
}

class GermanGreetings extends Greetings with  DefaultGreetings {
 override def sayHello: String = "Guten Tag" 
}

val g = new GermanGreetings
g.sayHello     // outputs Guten Tag
g.defaultHello // outputs Hello
</code></pre>

Traits can also be mixed-in at the instance level:

<pre><code>val j = new JapaneseGreetings with DefaultGreetings 
j.sayHello     // outputs konnichiwa 
j.defaultHello // outputs Hello
</code></pre>
