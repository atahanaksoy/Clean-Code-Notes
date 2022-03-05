# Chapter 2: Meaningful Names

## Use Intention-Revealing Names

The name of a variable, function, or class, should answer: why it exists, what it does, how it is used.

> If a name requires a comment, then the name does not reveal its intent.

```java
int d; // elapsed time in days

// Instead, name as below:

int elapsedTimeInDays;
int daysSinceCreation;
```

## Avoid Disinformation

We should avoid words whose entrenched meanings vary from our intended meaning.

Do not refer grouping of accounts as an `accountList` unless it's actually a list. The word list is something specific to programmers. If it's actually not a `List`, it may lead to false conclusions. So `accountGroup` would be better.

Beware of using names which vary in small names. For example, it's hard to notice the difference between `XYZControllerForEfficientHandlingOfStrings` and `XYZControllerForEfficientStorageOfStrings`.

## Make Meaningful Distinctions

Because you can't use the same name to refer two different things in the same scope, you might be tempted to change one name in an arbitrary way. (Sometimes by adding a character, misspelling one, etc.)

> It's not sufficient to add number series or noise words. If names must be different, then they should also mean something different.

### Number-series naming

Number-series naming (a1, a2, a3,...) is the opposite of intentional naming. They provide no clue.

```java
// Instead of this
public static void copyChars(char a1[], char a2[]) {}

// This function reads much better
public static void copyChars(char source[], char destination[]) {}
```

### Noise Words

Noise words are another meaningless distinction. Imagine you have `Product` class, 
if you also have `ProductInfo` or `ProductData`, you have made the names different but without making them mean anything different. Words such as `Info` and `Data` are indistinct noise words.

> Distinguish names in such a way that the reader knows what the differences offer.

## Use Pronounceable Names

If you can't pronounce the name, you can't discuss it without sounding like an idiot.

```java
// Instead of below (generation date, year, month, day, hour, minute, seconds)
private Date genymdhms;

// Use below:
private Date generationTimestamp;
```

## Use Searchable Names

Single-letter names or numeric constants have a particular problem in that they are not easy to locate across a body of a text.

> Single letter names can ONLY be used as local variables inside short methods. *The length of a name should correspond to the size of its scope*.

```java
// Instead of below:
for (int j=0; j<34; j ++) {
    s += (t[j] * 4) / 5 ;
}

// Use below:
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;

for (int j=0; j < NUMBER_OF_TASKS; j++) {
    int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
    int realTaskWeeks = realDays / WORK_DAYS_PER_WEEK;
    sum += realTaskWeeks;
}
```

Even though intentionally named code makes for a longer function, consider how much easier it will be to find `WORK_DAYS_PER_WEEK` than to look where `5` was used.

## Avoid Encodings

Encoding type or scope information into names simply adds an extra burden of deciphering. 

Especially in strongly-typed languages (such as Java), you don't need type-encoding. (e.g. `PhoneString` is useless)

You also don't need to prefix member variables with `m_` anymore. Your classes and functions should be small enough that you don't need them. And your editing environment would highlight the differences.

```java
// Instead of this:
public class Part {
    private String m_dsc;

    void setName(String name) {
        m_dsc = name;
    }
}

// Do this:
public class Part {
    private String description;

    void setDescription(String description) {
        this.description = description;
    }
}
```

Another encoding is when we have an interface and it's implementation. For example:

```
src/IShapeFactory.java --> Interface
src/ShapeFactory.java --> Implementation
```

Instead of encoding the interface, prefer encoding the implementation as this way the users wouldn't know that you are handing them an interface:

```
src/ShapeFactory.java --> Interface
src/ShapeFactoryImp.java --> Implementation
```

## Class Names

Classes and objects should have noun or noun phrase names like `Customer`, `WikiPage`, `AddressParser`, etc. Avoid words like `Manager`, `Processor`, `Data`, `Info` in the name of a class.

> **A class name should not be a verb.**

## Method Names

Methods should have verb or verb phrase names like `postPayment`, `deletePage`, `save`. Accessors, mutators and predicates should be named for their value and prefixed with `get`, `set`, and `is`.

```java

employee.getName();
employee.setName("mike");
if (paycheck.isPosted()) {..
```

When constructors are overloaded, use static factory methods rather than using the constructors itself (make the constructor private and instead implement a static method)

```java
// Do this
Complex fulcrumPoint = Complex.FromRealNumber(23.0)

// Instead of this
Complex fulcrumPoint = new Complex(23.0);
```

## Don't be Cute

If names are too clever, they will be memorable only to people who share the author's sense of humor, and only as long as these people remember the joke. So don't name a function `holyHandGrenade` for `deleteItems`.

## Pick One Word per Concept

Pick one word for one abstract concept. For instance, it's confusing to have `fetch`, `retrieve`, `get` as equivalent methods of different classes.

Similarly, it's confusing to have `Controller`, `Manager`, `Driver` in the same codebase. What is the essential difference between `DeviceManager` and `ProtocolController`? Why are both not `controllers` or both not `managers`? The name leads you to expect two objects that have very different type as well as having different classes.

## Don't Pun

Following pick one word per concept, don't use the same word for two purposes. If `add` method creates a new value by adding or concatenating two existing values in one class, and if we were to create a new method that appends a value to an array, don't use `add`, but use names such as `insert`.

## Use Solution Domain Names

People who read your code will be programmers, so go ahead and use CS terms. `AccountVisitor` means a great deal to a programmer who is familiar with the Visitor pattern. What programmer would not know what a `JobQueue` is?

## Use Problem Domain Names

When there is no "programmer-eese" for what you are doing, use the name from the problem domain. At least the programmer who maintains your code can ask a domain expert what it means.

## Add Meaningful Context

There are a few names which are meaningful in and of themselves - most are not. Instead, **you need to place names in context for your reader by enclosing them in well-named classes, functions or namespaces. When all else fails, then prefixing the name may be necessary as last resort.**

Imagine that you have variables named `firstName`, `lastName`, `street`, `houseNumber`, `state`, etc. Taken together, they form an address. But what if you just saw `state` variable used alone in a method? Would you automatically infer that it was part of an address?

You can add prefixes to add more context (e.g `addrState`), but a better solution would be to create a wrapper class named `Address`.

## Don't Add Gratuitous Context

In an imaginary application called "Gas Station Deluxe", it is a bad idea to prefix every class with "GSD".

Likewise, say you invented a "MailingAddress" class in "GSD"s accounting module, and you named it "GSDAccountAddress". 10 of 17 characters are redundant.

> Add no more context to a name than is necessary.

The names `accountAddress` and `customerAddress` are fine names for instances of class `Address` but could be poor names for classes.
