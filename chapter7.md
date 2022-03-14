# Chapter 7: Error Handling

## Use Exceptions Rather Than Return Codes

Back in the distant past there were many languages that didn't have exceptions. In those, the technique for error handling was to return an error flag or code.

The worst part is the caller has to check for errors immediately after the call; and it is easy to forget.

Therefore, it is better to throw an exception when you encounter an error.

## Use Unchecked Exceptions

> Checked Exception: The signature of every method would list all of the exceptions that it could pass to its caller.

In checked exceptions, if the lower level function is changed (let's say it throws a new exceptions), then the above functions would also have to append the new exception to their `throws` signature. **This violates the Open/Closed principle**. Because

## Provide Context with Exceptions

Each exception that you throw should provide enough context to determine *the source* and *location* of an error.

## Define Exception Classes in Terms of a Caller's Needs

The most important concern when we define an exception is *how they are caught*.

If your *try-catch-finally* block contains a lot of duplication, if the work is roughly the same, simplify the code by wrapping the API that you call.

For example, instead of below:

```java
ACMEPort port = new ACMEPort(12);

try {
    port.open();
} catch(DeviceResponseException e) {
    reportPortError(e);
    logger.log("...")
} catch (ATM1212UnlockedException e) {
    reportPortError(e);
    logger.log("...")
} catch {....}
```

Do below:

```java
LocalPort port = new LocalPort(12);
try {
    port.open();
} catch (PortDeviceFailure e) {
    reportError(e);
    logger.log(e.getMessage(), e);
}
```

Here we used a custom wrapper called `LocalPort` that translates exceptions thrown from `ACMEPort`.

Wrapping third-party APIs is a best practice:

- Minimizes dependency to third-party API. You can move to a different library without much penalty.
- You can define your own API without being tied to a particular vendor.

## Define the Normal Flow

There are some times when you may not want to abort when an exception is thrown.

Look at below code:

```java
try {
    MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
    m_total += expenses.getTotal();
} catch(MealExpensesNotFound e) {
    m_total += getMealPerDiem();
}
```

Here, when meal is expensed, they become part of the total. If they aren't, the employee gets a meal per diem. **The exception clutters the logic**.

Thus, you can change the `ExpenseReportDao` so that it always returns a `MealExpense` object. (i.e handling this logic in a wrapper)

```java
public class PerDiemMealExpenses implements MealExpenses {
    public int getTotal() {
        // return the per diem by default
    }
}
```

## Don't Return Null

```java
ItemRegistry registry = persistentStore.getItemRegistry();
if (registry != null) {
    ....
}
```

When we return `null`, we are essentially creating work for ourselves and foisting problems upon our callers. Therefore, throw errors or return a special case object. For example, instead of returning `null` for a list, return an empty list.

## Don't Pass Null

Similar to above, passing `null` should be avoided at all costs. In most programming languages there is no good way to deal with a `null` that is passed by a caller. Therefore, it must be forbidden to pass it.
