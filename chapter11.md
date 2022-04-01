# Chapter 11: Systems

## Separate Constructing a System from Using It

Software systems should separate the startup process -when the application objects are constructed and the dependencies are "wired" together- from the runtime logic that takes over after startup.

```java
public Service getService() {
    if (service == null) {
        service = new MyServiceImpl(...);
    }
    return service;
}
```

The above example results with faster startup; however, we now have a hardcoded dependency on `MyServiceImpl` and everything its constructor requires. We can't compile without resolving these dependencies.

Therefore, we should separate the runtime logic from the dependency resolution.

### Separation of Main

One way to separate *construction* from *use* is to move all construction to *main*, or modules called by *main*; and design the rest of the system knowing that all objects have been constructed.

### Factories

Sometimes we need to make the application respoknsible for *when* an object gets created. In such cases, use **Abstract Factory Pattern** to keep the details of construction separate from the application code.

### Dependency Injection

A class can create an instance of the MyDependency class to make use of its WriteMessage method. In the following example, the MyDependency class is a dependency of the IndexModel class:

```c#
public class IndexModel : PageModel
{
    private readonly MyDependency _dependency = new MyDependency();

    public void OnGet()
    {
        _dependency.WriteMessage("IndexModel.OnGet");
    }
}
```

Code dependencies, such as in the previous example, are problematic and should be avoided for the following reasons:

- To replace MyDependency with a different implementation, the IndexModel class must be modified.
- If MyDependency has dependencies, they must also be configured by the IndexModel class. In a large project with multiple classes depending on MyDependency, the configuration code becomes scattered across the app.
- This implementation is difficult to unit test.

Dependency injection addresses these problems through:

- The use of an interface or base class to abstract the dependency implementation.
- Registration of the dependency in a service container. ASP.NET Core provides a built-in service container, IServiceProvider. Services are typically registered in the app's Program.cs file.
- Injection of the service into the constructor of the class where it's used. The framework takes on the responsibility of creating an instance of the dependency and disposing of it when it's no longer needed.

