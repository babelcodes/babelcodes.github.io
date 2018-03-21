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
---

* TOC
{:toc}

## Main topics

* [Constants](/Constant), [Variables](/Variable) and [Optionals](/Optional)

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
