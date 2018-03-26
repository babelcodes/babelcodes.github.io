---
layout: feature
name: 'Type Unit'
iid: TypeUnit
status: DONE
language: scala
abstract: "Type like `void`"
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
 - Constant
 - Variable
 - Function
---

`Unit` serves the same purpose as `void` in languages like Java or C:

```
object MyModule {
  def main(args: Array[String]): Unit = 
    println(args[0])
  }
}
```