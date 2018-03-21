---
layout: feature
name: 'Class'
iid: Class
status: DOING
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
features_:
 - AccessControl
 - ClassMethod
 - Closure
 - Enumeration
 - Extension
 - Function
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

<pre><code>
def estimatedEffort(servings:Int): Int = {
println("estimating the effort...")
servings * cookTime * calories }
</code></pre>
