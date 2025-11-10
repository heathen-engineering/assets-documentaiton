# Lambda Expression

Lambda expressions (often just “expressions”) are a concise way to define inline functions. They’re especially useful when creating predicates for searching lists, defining callbacks for asynchronous calls, or managing scope-sensitive data. By embedding the function logic directly where it’s used, lambdas improve clarity and maintainability in your game code.

### Overview

Lambda expressions allow you to create anonymous functions without the overhead of a full method declaration. In many programming languages, the syntax follows this general pattern:

```
[capture](parameters) -> return_type {
    // function body
};
```

They offer benefits such as:

* **Conciseness:** No need for verbose method declarations.
* **Flexibility:** Ideal for callbacks, predicates, and inline data processing.
* **Scope Management:** Capture only the necessary external variables.

### Syntax and Semantics

In C++, for example:

```cpp
auto add = [](int a, int b) -> int {
    return a + b;
};
int result = add(3, 4);  // result is 7
```

And in C#:

```csharp
Func<int, int, int> add = (a, b) => a + b;
int result = add(3, 4);  // result is 7
```

These examples show how lambdas encapsulate a function body and can be passed around as objects.

### Unity Example: Lambda Expressions in C\#

In Unity, lambda expressions streamline common tasks such as callbacks, predicates, and simple inline property getters. Here are a few practical examples:

#### Predicates and Searching

Instead of defining a separate method to find a GameObject by name, you can use a lambda expression with LINQ:

```csharp
using System.Linq;
using UnityEngine;
using System.Collections.Generic;

public class LambdaExample : MonoBehaviour
{
    public List<GameObject> objects;

    void Start()
    {
        var target = objects.FirstOrDefault(p => p.name == "OMG so cool!");
        if (target != null)
            Debug.Log("Found it!");
        else
            Debug.Log("No GameObject by that name.");
    }
}
```

This inline predicate (`p => p.name == "OMG so cool!"`) is equivalent to writing a separate method for the search, but with much less boilerplate.

#### Callback Example

For asynchronous calls or handling events, lambdas let you define callbacks in place:

```csharp
public void DoSomething(System.Action<string, int> callback)
{
    // Some asynchronous work...
    callback?.Invoke("Result", 42);
}

// Calling the method with a lambda:
DoSomething((message, value) =>
{
    Debug.Log(message + " and " + value.ToString());
});
```

This approach improves code readability by keeping the callback logic close to where it is used.

### Unreal Example: Lambda Expressions in C++

Unreal Engine (UE4/UE5) also supports lambda expressions, which can simplify code for tasks such as sorting, filtering, or handling asynchronous operations.

#### Sorting Game Entities

Suppose you want to sort an array of game entities based on a custom criteria. With lambdas, you can define the comparator inline:

```cpp
#include "YourGameHeader.h"
#include <algorithm>

TArray<AActor*> Actors = /* Assume this is populated */;
Actors.Sort([](const AActor& A, const AActor& B)
{
    // For example, sorting by distance from a specific point
    const FVector ReferencePoint(0.0f, 0.0f, 0.0f);
    return A.GetActorLocation().Distance(ReferencePoint) < B.GetActorLocation().Distance(ReferencePoint);
});
```

This lambda defines a comparator directly within the `Sort` call, keeping your code succinct.

#### Asynchronous Tasks

When using Unreal’s asynchronous systems, such as timers or delegates, lambdas can be used to define inline behavior:

```cpp
FTimerHandle TimerHandle;
GetWorld()->GetTimerManager().SetTimer(TimerHandle, []()
{
    UE_LOG(LogTemp, Log, TEXT("Timer expired, executing lambda callback."));
}, 2.0f, false);
```

This lambda is executed once after a 2-second delay, reducing the need for separate callback methods.

### Best Practices

* **Capture Minimal Scope:** Only capture variables you need to avoid unintended side effects.
* **Keep It Focused:** If the lambda grows too complex, consider a named function for clarity.
* **Avoid Overuse:** While lambdas simplify code, overuse—especially in performance-critical sections—can lead to increased garbage collection or harder-to-debug code.

### Conclusion

Lambda expressions are a powerful tool across multiple game development platforms. In Unity, they simplify event handling and predicate creation, while in Unreal, they help manage custom sorting and asynchronous operations. By leveraging lambdas appropriately, you can write cleaner, more modular code that keeps related logic in one place.
