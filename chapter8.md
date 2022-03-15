# Chapter 8: Boundaries

We sometimes use third party libraries/packages, or software components from other teams; and we must cleanly integrate this foreign code to our own.

## Using Third-Party Code

Third party packages and frameworks strive for broad applicability so they can appeal to a wide audience. However, users want an interface that is focused on their particular needs.

For example, `java.util.Map` has many capabilities such as below:

```java
clear() void - Map
containsKey(Object key) boolean - Map
...
```

However, this brings a problem. Now every user has a power to clear the *Map*. Or, it doesn't constrain a type of object. Any user can add items of any type.

Therefore, instead of below:

```java
Map sensors = new HashMap();
Sensor s = (Sensor)sensors.get(sensorId);

// or below (which fixes the problem of type-casting)
Map<Sensor> sensors = new HashMap<Sensor>();
Sensor s = sensors.get(sensorId);
```

Do below:

```java
public class Sensors {
    private Map<Sensor> sensors = new HashMap<Sensor>();

    public Sensor getById(String id) {
        return sensors.get(id);
    }
    ...
}
```

The interface at the boundary (*Map*) is now hidden. Type management is handled in the class.

> You don't have to do this for each *Map*, only when you have to pass *Map* around your system. It's okay if you keep it inside the class, or close family classes.

- The code is now easier to understand and harder to misuse.
- This boundary constrained the interface to meet the needs of the application.

## Exploring and Learning Boundaries

To learn about third-party code, instead of spending time to read documentation or trying to integrate it to our code, **write the tests for it.**

These tests are called learning tests and they are beneficial because:
- It helps our understanding.
- We can run the tests to see if anything changed with the new update of the third-party code.
- It verifies the expected behavior.

## Using Code That Does Not Yet Exist

If API for a dependency is not been designed yet, you can write your own interface and specify what you want from the boundary interface. After API evolves, you can integrate it to your interface. You can also utilize *Adapter Pattern* to convert from your own interface to the provided one.
