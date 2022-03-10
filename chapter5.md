# Chapter 5: Formatting

## Vertical Formatting

Small files are easier to understand than large files are. Therefore, even though it's not a rule, *keeping files **on average 200 lines long** (500 lines at most) is desirable.*

### The Newspaper Metaphor

A well-written newspaper article will be read vertically and at the top you expect a headline that will tell you what the story is about and allows you to decide whether its something you want to read. As you continue down the details will increase until you have all the information.

A source file should be like a newspaper article. 

- The name of a source file should be simple yet explanatory.
- The name should be sufficient enough to tell us whether we are in the right module or not.
- The topmost part of the source file should provide high-level concepts and algorithms.
- Details should increase as we move downward, until we find the lowest level of functions and details in the bottom.

### Vertical Openness Between Concepts

*Each blank line is a visual cue that identifies a new and separate concept.*

### Vertical Density

If vertical openness separate concepts, then vertical density implies close association. *Lines of code that are tightly related should appear vertically dense.*

### Vertical Distance

*Concepts that are closely related should be kept vertically close to each other.* Clearly this rule doesn't work when concepts belong in separate files. **But then closely related concepts should not be separated into different files unless you have a very good reason.**

> We want to avoid forcing readers to hop around through our source file and classes.

#### Variable Declarations

- **Variables should be declared as close to their usage as possible**. Because our functions are very short, local variables should appear at the top of each function.

    ```java
    private static void readPreferences() {
        InputStream is = null;
        try {
            is = new FileInputStream(getPreferencesFile());
            ...
        }
    }
    ```
- Control variables for loops should usually be declared within the loop statement.

    ```java
    for (Test each: tests) {
        count += each.countTestCases();
    }
    ```
- Instance variables should be declared at the top of the class.
- **If one function calls another, they should be vertically close, and the caller should be above the callee**, if at all possible.
- Certain bits of code have a certain *conceptual affinity* with other bits. The affinity may base on direct dependence (one function calling another), or a function using a variable. But affinity may also be caused because a group of functions perform a similar operation. For example below functions have a strong conceptual affinity as they share a common scheme and perform variations of the same basic task.

```java
public class Assert {
    static public void assertTrue(String message, boolean condition) {
        ...
    }
    
    static public void assertFalse(String message, boolean condition) {
        ...
    }

    static public void assertFalse(boolean condition) {
        ...
    }
}
```

## Horizontal Formatting

We should strive to keep our lines short. **Ideally, 80, at max 120 characters per line.**

### Horizontal Openness and Density

We use horizontal white space to associate things that are strongly related and disassociate things that are more weakly related.

- Assignment operators should be surrounded with white space since they have two distinct and major elements.

    ```java
    // Instead of this
    int lineSize=line.length();
    // Do this
    int lineSize = line.length();
    ```

- Use whitespace to accentuate the precedence of operators. Notice how nicely the below equations are read. The terms are separated by white space because addition and substraction are lower precedence.

    ```java
    return (-b + Math.sqrt(determinant)) / (2*a);
    // or
    return b*b - 4*a*c;
    ```

### Indentation

### Breaking Indentation

It is sometimes tempting to break indentation rule for short `if` , `while`, or short functions. **But avoid breaking the indentation rule.**
