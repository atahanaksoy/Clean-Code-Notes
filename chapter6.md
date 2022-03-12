# Chapter 6: Objects and Data Structures

## Data Abstraction

> Hiding implementation is not just a matter of putting a layer of functions between the variables. Hiding implementation is about abstractions!

A class should expose abstract interfaces that allow its users to manipulate the essence of the data, without having to know its implementation.

```java
// Instead of this
public interface Vehicle {
    double getFuelTankCapacityInGaloons();
    double getGalloonsOfGasoline();
}

// Do this as we don't want to expose the details of our data.
// Rather we want to express our data in abstract terms (percentage).
public interface Vehicle {
    double getPercentFuelRemaining();
}
```

## The Law of Demeter

> A method should not talk to "strangers", but only "friends".

A method `f` of a class `C` should only call the methods of these:

- C
- An object created by `f`
- An object passed as an argument to `f`
- An object held in an instance variable of `C`

The below code violates this law as it talks to the return value of `ctxt.getOptions()` and so on.

```java
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```

### Train Wrecks

This kind of code is often called a *train wreck* because it looks like a bunch of coupled train cars.

> Chain of calls should be avoided.

Instead;

```java
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

However, this still violates the *Law of Demeter* if the return value of these functions are objects. If they are objects, then their internal structure should be hidden rather than exposed. (we shouldn't know about the internals of `opts` or others).

So instead, we should implement a function in `ctxt` which would prevent the current function from having to vioalte the law and navigating through objects it shouldn't know about.

### Hybrids

Avoid implementing hybrid structures that are half object and half data structure. 

> Data structures should not have any business logic but should only contain data. On the other hand, objects contain business logic.

## Data Transfer Objects 

The best form of a data structure is a class with public variables and no functions. This is sometimes called a data transfer object, or DTO. DTOs are very useful when communicating with databases or parsing messages from sockets.
