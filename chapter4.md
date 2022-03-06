# Chapter 4: Comments

**Comments are always failures.** When you find yourself in a position where you need to write a comment, think it through and see whether there isn't some way to turn the tables and express yourself in code.

> Too often, the comments lie. Code changes and evolves and programmers can't maintain them.

## Comments Do Not Make Up for Bad Code

Clear and expressive code with few comments is far superior to cluttered and complex code with lots of comments. *Rather than spending your time writing the comments of the mess, spend it cleaning the mess.*

## Explain Yourself in Code

It takes only few seconds of thought to explain most of your intent in code. 

> In many cases, it's simply a matter of creating a function that says the same thing as the comment you want to write.

Instead of this:
```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && employee.age > 65) {..
```
Do this:
```java
if (employee.isEligibleForFullBenefits()) {..
```

## Good Comments

- **Legal Comments**: The copyright and authorship statements that are necessary to put into a comment at the start of each source file. *If possible, refer to a standard license or other external document rather than putting all the terms and conditions into the comment.*

- **Informative Comments**: It is sometimes useful to provide basic information with a comment. For example commenting the format that is being matched from a regular expression.

- **Explanation of Intent**: Sometimes a comment provides the intention behind a decision. These comments are helpful to understand what the author was trying to do.

- **Clarification**: Sometimes it is helpful to translate the meaning of some obscure argument or return value into something that's readable when they are a part of the standard library or vendor and you cannot alter the code.

- **Warning of Consequences**: Sometimes it is useful to warn other programmers about certain consequences.

- **`TODO` Comments**: `TODO`s are jobs that the programmer thinks should 
be done, but for some reason can't do at the moment. Still, you don't want your code to be littered with `TODO`s. Scan them regularly and eliminate the ones you can.

- **Amplification**: A comment may be used to amplify the importance of something that may otherwise seem inconsequential.

## Bad Comments

- **Mumbling**: If you decide to write a comment, then spend time necessary to make sure it is the best comment you can write (Don't leave an enigma)

- **Redundant Comments**: Comments as `javadocs` are redundant. They are not more informative than the code. They do not justify, provide intent or rationale.

    ```java
    /**
    * The processor delay for this component.
    */
    protected int backgroundProcessorDelay = -1;
    ```

- **Misleading Comments**: Sometimes a programmer makes a statement in his/her comments that isn't precise enough to be accurate.

- **Mandated Comments**: It is just plain silly to have a rule that says that every function must have a `javadoc`. Comments like these clutter up the code, propogate lies, and lend to general confusion and disorganization.

    ```java
    /**
    * @param title The title of the CD
    * @param author The author of the CD
    * @param tracks The number of tracks on the CD
    * @param durationInMinutes The duration of the CD in minutes
    */
    public void addCD(String title, String author, int tracks, int durationInMinutes);
    ```

- **Noise Comments**: Sometimes you see comments that are nothing but noise. They restate the obvious and provide no new information.

- **Position Markers**: Sometimes programemrs like to mark a particular position in a source file. For example:
    ```java
    // Actions ///////////////////
    ```
    They rarely make sense to gather certain functions together. But in general they are clutter that should be eliminated.

- Closing Brace Comments

- **Commented-Out Code**: *DON'T DO THIS!*. Others who see that commented-out code won't have the courage to delete it. We have source control systems and they will remember the code for us.

- **Nonlocal Information**: If you must write a comment, then make sure it describes the code it appears near. Don't offer systemwide information in the context of a local comment.

- **Too Much Information**: Don't put interesting historical discussions or irrelevant descriptions of details into comments.

- **Inobvious Connection**: The purpose of comment is to explain code that does not explain itself. It is a pity when a comment needs its own explanation.
