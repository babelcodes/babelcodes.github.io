---
layout: feature
name: 'Class'
iid: Class
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
 - Trait
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

## Introduction

Scala is a pure object-oriented language. Conceptually, every value is an object and every operation is a method call.

<pre><code>// src/main/scala/Recipe.scala
class Recipe(calories: Int) {
  println(s"Created recipe with ${calories} calories") 
  
  var cookTime: Int = 0
}
</code></pre>

> This creates a Scala class called Recipe with a constructor that takes calories as a parameter.

See also "primary constructor" and "secondary constructors".

By default:
- the constructor parameters for a class are only visible inside the class itself 
- and only values and variables are visible outside of the class

<pre><code>// src/main/scala/Hello.scala
val r = new Recipe(100) // outputs Created recipe with 100 calories
println(r.cookTime)     // outputs 0
r.cookTime = 2
println(r.cookTime)     // outputs 2
println(r.calories)     // This will produce an error - value calories is not a member of recipe
</code></pre>


Promote constructor parameters with prefix `val` or `var`:

<pre><code>// src/main/scala/Recipe.scala
class Recipe(val calories: Int) {
  ...
}

val r = new Recipe(100)
println(r.calories)     // Now that works!
</code></pre>


## Methods

Method definitions in Scala start with the keyword `def` followed by the name of the method and its parameters. 

The return type of the method can be [inferred](/functional/TypeInference), just like with [Variables](Variable), when not explicitly declared.

<pre><code>def estimatedEffort(servings:Int): Int = {
  println("estimating the effort...")
  servings * cookTime * calories 
}
</code></pre>


## Inheritance

We can create subclasses by extending abstract or non-final classes.

One difference is the constructor parameters of the class being extended need to be passed in as well.

<pre><code>class Food(calories: Int)
class Salad(val lettuceCalories: Int, val dressingCalories: Int)
extends Food(lettuceCalories + dressingCalories)
</code></pre>

When extending a class we can also override members of parent classes:

<pre><code>// Example of Overriding Methods 
class Menu(items: List[Food]) {
  def numberOfMenuItems() = items.size 
}

// Dinners only consists of Salads
class Dinner(items: List[Salad]) extends Menu(items) {
  // Overriding def as val
  override def numberOfMenuItems = 2 * items.size 
}

val s1 = new Salad(5, 5)
val s2 = new Salad(15, 15)
val dinner = new Dinner(List(s1, s2))

// prints 4
println(s"Number Of Menu Items = ${dinner.numberOfMenuItems}")
</code></pre>


## Companion objects with apply

Scala does not have a `static` keyword like Java to mark a definition as a static (singleton) instance. Instead it uses 
the `object` keyword to declare a singleton object.

For example the `App` main class is an `object`:

<pre><code>// src/main/scala/Hello.scala
object Hello extends App { 
  println("Hello, World!")
}
</code></pre>

Objects are commonly used:
- for declaring constants
- to hold factory methods for creating classes

This last pattern is so common that Scala declares a special method definition for this, called `apply()`. It can be thought
of like a default factory method that allows the object to be called like a method:

<pre><code>// src/main/scala/Recipe.scala
object Recipe {
  def apply(calories :Int) = new Recipe(2 * calories)
}

val r1 = Recipe.apply(100) // This call refers to the Recipe object
val r2 = Recipe(200)       // apply method is called by default
println(r2.calories)       // outputs 400
</code></pre>

An object is considered a __companion object__ when it is declared in the same file as the class and shares the name and 
the package. Companion objects are used to hold the static definitions related to class but do not have any special relationship 
to a class.


## Case class

A case class has one to many named attributes and provides several built-in functions automatically generated by the compiler
to reduce the amount of code for common tasks: use the `case` keyword before the class definition.

A case class is immutable.

When you declare a class as a case class, the Scala compiler automatically generates:
- a default constructor, with parameters immutable (by using `val` keyword)
- `equals`, `hashCode`, and `toString` are generated based on the constructor parameters
- a copy constructor
- a companion object and the default apply factory method is created
- an accessor for each attribute
- [Pattern Matching](/functional/PatternMatching) on the class is made possible

```
   case class Person(name: String, age: Int)
   
   val m1 = new Person("Mikael", 41)     // 'new' is optional...
   val m2 = Person("Mikael", 41)         // ... because apply method of the companion object can be used
   mikael == mikaelNew                   // == compares values, not references
   mikael.equals(mikaelNew)              // == is exactly the same as .equals
   val name = mikael.name
   // mikael.name = "Nicolas"            // does not compile (immutable)
   val n = mikael.copy(name = "Nicolas") // need to create a copy
```


## Traits

Traits can be viewed as an interface that provides a default implementation of some of the methods.

See [Trait](Trait) section.