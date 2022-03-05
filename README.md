# Chapter 1: Clean Code

## There Will Be Code

Code is the language in which we ultimately express the requirements. Even though we can create langauges that are closer to those requirements (level of abstractions in coding languages will increase), there will never be a perfect machine that could eliminate the need of code.

> No machine can eliminate the need of code.

## Bad Code

We wade thorugh bad code. We struggle to find our way, hoping for some hint, some clue, of what is going on; but all we see is more senseless code.

We tend to write bad code when 

- we are in rush, 
- we have a lot of backlog items that needs to be done,
- we decide working mess is better than nothing, and we promise to clean it up later.

> Later equals never, so never write bad code.

## The Total Cost of Owning a Mess

Over the span of year or two, teams that were moving very fast at the beggining of a project can find themselves moving at a snail's pace. Every change they make to the code breaks two or three other parts of the code. No change is trivial. Every addition or modification to the system requires that the thangles, twists and knots to be "understood", which drives the productivity toward zero.

The management will then hire more people to increase the productivity but the new staff won't be able to understand the system. Eventually, the team will uprise and inform the management for a redesign, which is very costly and time consuming.

> The only way to make the deadline is to keep the code as clean as possible.

### What is Clean Code?

- *Pleasing to read (it should be readable just as a novel).*
- *Should contain only what is necessary. (minimal)*
- *Focused, each function, each class each module exposes a single responsibility.*
- *Should be enhancable by other developers.*
- *Should have tests.*
- *Should look like that the code has been taken care of to keep it simple and orderly.*
- *Should not have duplications, instead, should have abstractions.*
- *Each line of code should be pretty much what you expected (i.e the code should be obvious)*

> Leave the campground cleaner than you found it.

If we all checked-in our code a little cleaner than when we checked it out, the code
simply could not rot.

<br/>

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

<br/>

# Chapter 3: Meaningful Names

## Small!

*The first rule of functions is that they should be small.* Each function should told a story and each should led you to the next in a compelling order.

### Blocks and Indenting

Blocks within `if`, `else`, `for`, `while` statements and so on should be one line long.

## Do One Thing

*Functions should do one thing. They should do it well. They should do it only.*

> If a function does only those steps that are one level below the stated name of the function, then the function is doing one thing.

A way to know that a function is doing more than "one thing" is if you can extract another function from it with a name that is not merely a restatement of its implementation.

## One Level of Abstraction per Function

In order to make sure our functions are doing "one thing", we need to make sure that the statements within our function are all at the same level of abstraction.

For example, in a function, there shouldn't be a high level abstraction such as `getHtml();`, then an intermediate level of abstraction such as `String pathName = pathParser.render(pagePath)`, and then a low level abstraction such as `.append("\n")`.

### Reading Code From Top to Bottom: The Stepdown Rule

*We want the code to read like a top-down narrative. We want every function to be followed by those at the next level of abstraction so that we can read the program, descending one level of abstraction at a time as we read down the list of functions.*

## Switch Statements

By their nature, `switch` staments always do *N* things. We can't always avoid `switch` statements, but we can make sure that each are buried in a low-level class and is never repeated.

Consider below code:

```java
public Money calculatePay(Employee e) throws InvalidEmployeeType {
    switch(e.type) {
        case COMMISSIONED:
            return calculateComissionedPay(e);
        case HOURLY:
            return calculateHourlyPay(e);
        case SALARIED:
            return calculateSalariedPay(e);
        default:
            throw new InvalidEmployeeType(e.type);
    }
}
```

There are several problems.

- It's large.
- Whenever new employee types are added, it will grow.
- It violates the Single Responsibility Principle because it does more than one thing.
- It violates Open Closed Principle because it must change whenever new types are added.

But the worst part is that there are an unlimited number of other functions that will have the same `switch` structure. For example we could have:

```java
isPayDay(Employee e, Date date);
deliverPay(Employee e, Money pay);
```

As a solution, try to bury the `switch` statement in the basement of an *Abstract Factory* as below:

```java
public abstract class Employee {
    public abstract boolean isPayDay();
    public abstract Money calculatePay();
    public abstract Money deliverPay(Money pay);
}

public interface EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
}

public class EmployeeFactoryImpl implements EmployeeFactory {
    
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType {
        switch(e.type) {
            case COMMISSIONED:
                return new CommissionedEmployee(r);
            case HOURLY:
                return new HourlyEmployee(r);
            case SALARIED:
                return new SalariedEmployee(r);
            default:
                throw new InvalidEmployeeType(e.type);
        }
    }
}
```

This way, `calculatePay`, `isPayDay`, `deliverPay` functions will be dispatched by polymorphically through the Employee interface.

## Use Descriptive Names

> The smaller and more focused the function is, the easier it is to choose a descriptive name.

*Don't be afraid to make a name long, a long descriptive name is better than a short enigmatic name, or a long descriptive comment.*

## Function Arguments

*The ideal number of arguments for a function is zero.* 

> **More than three arguments requires a very special justification.**

- The argument is at a different level of abstraction than the function name and forces you to know a detail that isn't particularly important at that point.
- Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that various combinations of arguments work properly.

### Common Monadic Forms

There are two very common reasons to pass a single argument into a function:

1. Asking a question about that argument (e.g `fileExists('myFile')`)
2. Operating on that argument (e.g. `InputStream openFile('myFile')`)

One less common single argument function is an *event*. The overall program is meant to interpret the function call as an event and use the argument to alter the state of the system, for example, `void passwordAttemptFailedNTimes(int attemps)`. *Use this form with care, it should be very clear to the reader that this is an event.*

**If a function is going to transform its input argument, the transformation should appear as the return value.** 

```java
// do this
StringBuffer transform(StringBuffer in) {}

// don't do this
void transform(StringBuffer out) {}
```

### Flag Arguments

**Passing a boolean into a function is a truly terrible practice.** It complicates the signature of the function, and it does more than one thing (does one thing if the flag is true, and another thing when the flag is false).

### Dyadic Functions

Two arguments are appropriate when they have a natural cohesion or a natural ordering. For example `Point p = new Point(0, 0)`, is perfectly reasonable.

However, functions like `assertEquals(expected, actual)` are problematic because these two arguments have no natural ordering.

Dyads aren't evil, but you should take advantage of what mechanisms may be avaiable to you to convert them into monads. For example:

```java
// Instead of this
writeField(outputStream, name)

// Implement it as below:
outputStream.writeField(name)

// or make outputStream a class variable and call it inside the function
writeField(name)
```

### Argument Objects

When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own. Consider below:

```java
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
```

> When groups of variables are passed together, they are likley part of a concept that deserves a name of its own.

### Argument Lists

Sometimes we want to pass a variable number of arguments into a function.

```java
public String format(String format, Object ...args)
```

If the variable arguments are all treated identically, then they are equivalent to a single argument of type *List*. By that reasoning, the above function is actually dyadic. 

Therefore, functions that take variable arguments can be monads, dyads or even triads; but it would a mistake to give them more arguments than that.

### Verbs and Keywords

A good function name should explain the intent of the function and the order and intent of the arguments.

For example:

```java
writeField(name) // tells us that name is a "field" that is "written".
assertExpectedEqualsActual(expected, actual) // tells us the ordering of the arguments
```

## Have No Side Effects

Side effects are lies. Your function promises to do one thing, but it also does other hidden things. It might make unexpected changes to the variables, parameters passed in the function, or system globals, etc.

### Output Arguments

In general, output arguments should be avoided. If your function must change the state of something, have it change the state of its owning object.

```java
// Instead of this
appendFooter(s) // we don't know whether this function appends footer to s, or adds s as a footer; so we check the signature

public void appendFooter(s) // so we learn that it appends footer to s

// do this (the object itself changes the state)
report.appendFooter()
```
## Command Query Separation

**Functions should either do something or answer something, but not both**. For example:

```java
/*
It could mean two things:

1- If the "username" field was previously set to "unclebob"; or
2- Set the "username" field to "unclebob" and if its succesful.

Therefore, instead of this:
*/
if (set("username", "unclebob")) ...

// Do this:
if (attributeExists("username")) {
    setAttribute("username", "unclebob");
}
```

## Prefer Exceptions to Returning Error Codes

Returning error codes from command functions is a violation of command query separation. When you return an error code, the caller must then deal with the error immediately.

```java
if (deletePage(page) == E_OK) {
    if (registry.deleteReference(page.name) == E_OK) {
        ....
    }
}
```

On the other hand, if you use exceptions instead of error codes, then the error processing code can be separated from the happy path code and can be simplified.

```java
try {
    deletePage(page);
    registry.deleteReference(page.reference);
} catch (Exception e) {
    logger.log(e.getMessage());
}
```

### Extract Try/Catch Blocks

Try/catch blocks mix error processing with normal processing. So **it is better to extract the bodies of the try and catch blocks out into functions of their own.**

So instead of above block, do this:

```java
try {
    deletePageAndAllReferences(page);
} catch (Exception e) {
    logError(e);
}

private void deletePageAndAllReferences(Page page) throws Exception {
    deletePage(page);
    registry.deleteReference(page.reference);
}

private void logError(Exception e) {
    logger.log(e.getMessage());
}
```

### Error Handling Is One Thing

Since functions should do one thing and error handling is one thing; if `try` keyword exists in a function, it should be the very first word and there should be nothing after the `catch/finally` blocks.

### Dependency Magnet

Returning error codes usually implies that there is some class or enum in which all the error codes can be defined:

```java
public enum Error {
    OK,
    INVALID,
    NO_SUCH,
    ...
}
```

Classes like these are *dependency magnet*, many other classes import and use it. Programmers tend to reuse the old codes instead of adding new ones that are more meaningful. 

Exceptions are derivatives of the exception class; they can be added without enforcing any recompiliation or redeployments.
