---
title: Design Patterns - Strategy pattern
subtitle: Strategy Pattern
tags: ['design patterns']
category: post
---

## Principles
- Encapsulate that varies. Identify the aspect of your application that vary and separate them from what stays the same.  
- Program to an interface(supertype), not an implementation.
- Favour composition over inheritence. HAS-A can be better than IS-A. Eg. Duck has a FlyingBehaviour

## Strategy pattern:
The Strategy Pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.
Enables the exact behaviour of a system to be selected at either run-time(dynamic) or compile-time(static).

<figure>
<img src="/assets/img/strategy_pattern.png" alt="strategy_pattern"
title="Strategy Pattern example" />
</figure>


## Reference
* Chapter 1: [Head First Design Patterns, 2nd Edition - *By Eric Freeman and Elisabeth Robson*](https://learning.oreilly.com/library/view/head-first-design/9781492077992/ch01.html)
