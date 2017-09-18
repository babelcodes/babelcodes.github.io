---
layout: programming
name: 'Reactive Programming'
iid: Reactive
status: DOING
abstract: ""
---

* TOC
{:toc}

## Introduction

Reactive Programming can be viewed as a Push programming model (vs. Pull) where everything is a database.

There are 3 main concepts:

1. __Observable__ that can an _Observer_ to call next on it
1. __Operators__ that map an Observable to another
1. __Subscription__ that map event to real world, with 3 callbacks:
  - one for each item
  - one for error handling
  - one for completion
