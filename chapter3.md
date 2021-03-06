# Chapter 3: Functions

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
