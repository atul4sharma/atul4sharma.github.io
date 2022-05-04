---
title: Design Patterns - Observer pattern
subtitle: Observer Pattern
tags: ['design patterns']
category: post
---

## Design Principle
- Strive for loosely coupled designs between objects that interacts. Loosely coupled designs allow us to build flexible OO systems that can handle change because they minimize the interdependency between objects.

## Observer pattern:
The Observer Pattern defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.
Observer is an object that wishes to be informed about events happening in the system. And the entity generating the event is called Observable.

<figure>
<img src="assets/img/observer_class_diagram.png" alt="observer_pattern"
title="Observer Pattern class diagram" />
</figure>


## Reference
* Chapter 2: [Head First Design Patterns, 2nd Edition - *By Eric Freeman and Elisabeth Robson*](https://learning.oreilly.com/library/view/head-first-design/9781492077992/ch02.html#the_observer_pattern_defined)
