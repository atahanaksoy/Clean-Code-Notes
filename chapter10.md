# Chapter 10: Classes

## Class Organization

A class should have below order:

1) Public static constants,
2) Public variables,
4) Private static variables,
5) Private instance variables

Public functions should follow the list of variables. Put the private utilities called by a public function right after the public function itself (for newspaper article alike reading experience).

### Encapsulation

Loosening encapsulation is always a last resort. In case if you have to test your private function, make it protected or package scoped.

## Classes Should Be Small!

The first rule of classes is that they should be small. We measure the size of a class by its *responsibilities*.

The name of a class should describe what responsibilities it fulfills. In fact, naming is probably the first way of helping determine class size. 

> If we can't name the class, then it's likely to be large. For example, Processor, Manager, Super often hint multiple responsibility.

We should be able to write the description of a class without using "if", "and", "or", "but". If we use them, then it means the class has too many responsibilities.

### The Single Responsibility Principle

A class should have one, and only one *reason to change*. We want our systems to be composed of many small classes, not a few large ones. 

Each small class encapsulates a single responsibility, has a single reason to change, and collaborates with a few others to achieve the desired system behaviors.

### Cohesion

Classes should have a small number of instance variables and each of the methods of a class should manipulate one or more of those variables.

> More variables a method manipulates, the more cohesive that method is to its class. Even though its not always possible, we would like to have high cohesion.

### Maintaining Cohesion Results in Many Small Classes

Let's say you want to extract a smaller part of a function into a separate function. And let's assume that the larger function has many variables that should also be used by the smaller functions. Should we pass each variable as a variable? NO! Make them instance variables, if it breaks cohesion, then create a separate class for that function.

## Organizing for Change

For most systems, change is continual. Every change subjects us to the risk that the remainder of the system no longer works as intended. In a clean system we organize our classes so as to reduce the risk of change.

> If private methods only relate to a subset of a class, it may indicate a possible abstraction.

Class should be open for extension but closed for modification (Open-Closed Principle).

## Isolating for Change

A client class depending upon concrete details is at risk when those details change. Therefore, introduce interfaces and abstract classes to help isolate the impact of those details. *Our classes should depend upon abstractions, not on concrete details* (Dependency Inversion Principle).
