---
layout: feature
name: 'Variable'
iid: Variable
status: DONE
language: scala
abstract: "Defines with 'var'. Can be modified"
_links:
 - link:
    name: 'The Swift Programming Language: A Swift Tour'
    url: https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/GuidedTour.html#//apple_ref/doc/uid/TP40014097-CH2-ID1
    description: ' - Apple Developer'
    type: reference
features:
 - Constant
---

Use `var` to make a variable.

<pre><code>// var myVariable :String = "hello"
var myVariable = "hello"
first = "Something Else"
</code></pre>

The Scala compiler has [inferred](/functional/TypeInference) `first` as a `String` because it was assigned a `String` value. 