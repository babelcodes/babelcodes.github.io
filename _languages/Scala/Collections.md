---
layout: feature
name: 'Collections'
iid: Collections
status: DONE
language: scala
abstract: ""
links_:
 - link:
    name: 'Swift API Reference: Generic Structure, Array'
    url: https://developer.apple.com/reference/swift/array
    description: ' - Apple Developer'
    type: reference
 - link:
    name: 'The Swift Programming Language: A Swift Tour'
    url: https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/GuidedTour.html#//apple_ref/doc/uid/TP40014097-CH2-ID1
    description: ' - Apple Developer'
    type: reference
features_:
 - Variable
 - Range
---

* TOC
{:toc}


The Scala collections library is one of the most powerful features of the language.

The library implements all the common data structures such as:
* sequences
* sets 
* maps (called dictionaries in some other languages). 

Scala collections come in many forms. They can be immutable, mutable and parallel. 

The language encourages you to use immutable collection APIs and imports them by default.

```
val marks = IndexedSeq(50, 70, 65)             // creates an index sequence

val numbers = Vector(11, 22, 33)               // creates sequence of numbers

val languages = Set("Scala", "Kotlin", "Java") // set of strings

// Creates a map with a key-value pairs
val nameAndGrades = Map("John" -> 'C', "Steve" -> 'A', "Mary" -> 'B')

val range = 0 to 10                            // range of all the numbers from 0 to 10
```


## Transforming

```
val xs = Vector(10, 20, 30, 40)
val halfs = mx.map(x => x / 2)   // executes the given anonymous function for each element

println(halfs)                   // Outputs new sequence Vector(5, 10, 15, 20)
println(xs)                      // outputs the original collection because it is immutable
```


## Filtering

```
val xs = Vector(1, 2, 3, 4, 5).filter(x => x % 2 != 0)  // Odd numbers
println(xs)                                             // outputs new collection Vector(1, 3, 5)
```


## Grouping

```
val groupByOddAndEven = Vector(1, 2, 3, 4, 5).groupBy(x => if (x % 2 == 0) "even" else "odd") 
println(groupByOddAndEven) // outputs Map(odd -> Vector(1, 3, 5), even -> Vector(2, 4))
```


## Sorting

```
val lowestToHighest = Vector(3, 1, 2).sorted 
println(lowestToHighest) // outputs Vector(1, 2, 3)
```


## Mutable

Scala provides mutable counterparts of all the immutable collections. 

For example, the following creates a mutable sequence of numbers:

```
val numbers = scala.collection.mutable.ListBuffer(10, 20, 30)
numbers(0) = 40         // updates the zeroth element to 40 
println(numbers)        // outputs ListBuffer(40, 20, 30)
```

## Traversable

Here are some of the useful methods defined in the `Traversable` trait that are available to all collection types:

<table class="table table-striped table-hover">
<thead><tr>
    <th>METHODS</th>
    <th>DSCRIPTION</th>
</tr></thead>

<tbody>
<tr>
    <td><code>.size</code></td>
    <td>The number of elements in the collection.</td>
</tr>
<tr>
    <td><code>xs ++ ys</code></td>
    <td>A collection consisting of the elements of both xs and ys.</td>
</tr>
<tr>
    <td><code>.map(f)</code></td>
    <td>The collection obtained from applying the function f to every element in xs.</td>
</tr>
<tr>
    <td><code>.flatMap(f)</code></td>
    <td>The collection obtained from applying the collection valued function f to every element in xs and concatenating the results.</td>
</tr>
<tr>
    <td><code>.filter(p)</code></td>
    <td>Returns a new collection consisting of those elements of xs that satisfy the predicate p.</td>
</tr>
<tr>
    <td><code>.find(p)</code></td>
    <td>An option containing the first element in xs that satisfies p, or None if no element qualifies.</td>
</tr>
<tr>
    <td><code>.foldLeft(z)(op)</code></td>
    <td>Apply binary operation op between successive elements of xs, going from left to right and starting with z as initial value.<br>
    <code>val x = Seq(1, 2, 3, 4)// sums all the numbersx. foldLeft(0){(a, e) => a + e}</code></td>
</tr>
<tr>
    <td><code>.foldRight(z)(op)</code></td>
    <td>Apply binary operation op between successive elements of xs, going from right to left and starting with z as initial value.</td>
</tr>
<tr>
    <td><code>.head</code></td>
    <td>The first element of the collection(or some element, if no order is defined).</td>
</tr>
<tr>
    <td><code>.tail</code></td>
    <td>The rest of the collection except xs.head</td>
</tr>
<tr>
    <td><code>.mkString(sep)</code></td>
    <td>Produces a string that shows all elements of xs between separators sep.</td>
</tr>
</tbody>
</table>
























