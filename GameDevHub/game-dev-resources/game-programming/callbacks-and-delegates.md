# Callbacks & Delegates

## Introduction

Callbacks and delegates are crucial programming patterns used widely in game development to manage asynchronous tasks, events, and complex state management. Whether in Unity, Unreal Engine, or other game engines, these tools allow developers to decouple different parts of the game code and handle dynamic events efficiently. In this article, we will explore how callbacks and delegates work and demonstrate examples in both C# (for Unity) and C++ (for Unreal Engine), highlighting how both engines make use of these concepts and expose them to their respective systems (such as Unity's Inspector and Unreal's Blueprint system).

## Understanding Callbacks and Delegates

### What is a Callback?

A **callback** is a function passed as an argument to another function. The receiving function can then call back the passed function at a later time, typically after completing some task. Callbacks are commonly used in asynchronous programming where operations like I/O, networking, or animations need to complete without blocking the main game loop.

* **Use Cases**: Callbacks are essential for handling events, managing async operations, and handling timing-based logic.

### What is a Delegate?

A **delegate** is a type-safe pointer to a method. It allows you to reference a method and pass it around, and then invoke it when needed. In C#, delegates are used for defining callback patterns, and in C++, they’re often used to create event-driven architectures.

* **Use Cases**: Delegates provide flexibility in handling dynamic events or callbacks in a type-safe manner, especially in object-oriented programming environments.

## Callbacks and Delegates in C\#

### Basic Example (C#):

In C#, delegates are typically used to implement callbacks. Here's a simple example that demonstrates a callback pattern.

```csharp
using System;

public class CallbackExample
{
    public void CallCallback()
    {
        Console.WriteLine("Starting task, calling callback...");
        ExecuteTask(TaskCompleteCallback);
    }

    public void ExecuteTask(Action callback)
    {
        // Simulate task completion
        Console.WriteLine("Task is completed.");
        callback?.Invoke(); // Invoke the callback once the task is complete
    }

    public void TaskCompleteCallback()
    {
        Console.WriteLine("Task callback invoked.");
    }
}
```

**Explanation**: The `ExecuteTask` method accepts a delegate (`Action callback`) and invokes it after completing the task. This is the fundamental pattern for callbacks in C#.

***

## Callbacks and Delegates in C++ (Unreal Engine)

In Unreal Engine, callbacks can be implemented using **delegates** and **events**. Delegates allow you to bind functions to events, which is particularly useful when exposing functionality to Blueprints.

### Basic Delegate Example (C++):

In Unreal Engine, delegates can be defined using the `DECLARE_DELEGATE` macro. Here's a simple C++ example to demonstrate the delegate concept.

```cpp
#include "CoreMinimal.h"
#include "Delegates/Delegate.h"

class FCallbackExample
{
public:
    DECLARE_DELEGATE(FTaskCompletedDelegate);  // Declare a simple delegate

    void CallCallback()
    {
        UE_LOG(LogTemp, Warning, TEXT("Starting task, calling callback..."));
        ExecuteTask(TaskCompleted);
    }

    void ExecuteTask(FTaskCompletedDelegate Delegate)
    {
        // Simulate task completion
        UE_LOG(LogTemp, Warning, TEXT("Task is completed."));
        Delegate.ExecuteIfBound(); // Execute the delegate if it's bound
    }

    void TaskCompleted()
    {
        UE_LOG(LogTemp, Warning, TEXT("Task callback invoked."));
    }
};
```

**Explanation**: The `FTaskCompletedDelegate` is declared using `DECLARE_DELEGATE`. When the task completes, `ExecuteIfBound()` is used to invoke the callback.

### Exposing to Blueprints (C++ Unreal Engine):

In Unreal Engine, you can expose delegates to Blueprints as events by using `BlueprintAssignable` or `BlueprintCallable`. This allows you to use the delegate system inside Unreal's Blueprint visual scripting system.

```cpp
UCLASS()
class MYGAME_API AMyActor : public AActor
{
    GENERATED_BODY()

public:
    UPROPERTY(BlueprintAssignable, Category = "Event")
    FTaskCompletedDelegate OnTaskCompleted;

    void ExecuteTask()
    {
        // Simulate task completion
        OnTaskCompleted.Broadcast();  // Broadcasts the event to any Blueprint listeners
    }
};
```

**Explanation**: In this example, `FTaskCompletedDelegate` is exposed as a `BlueprintAssignable` property, which allows Blueprints to bind functions to this event. In the Blueprint editor, you can connect the `OnTaskCompleted` event to a Blueprint node and handle the event visually.

## Passing Parameters with Callbacks and Delegates

#### Passing Parameters in C# Callbacks:

You can pass parameters to a callback in C# by defining the delegate with the desired parameter types.

```csharp
public void CallCallbackWithParameters()
{
    ExecuteTaskWithParameters((message, code) => {
        Console.WriteLine($"Message: {message}, Code: {code}");
    });
}

public void ExecuteTaskWithParameters(Action<string, int> callback)
{
    // Simulate task completion
    Console.WriteLine("Task is completed.");
    callback?.Invoke("Task Complete", 200);  // Passing parameters to the callback
}
```

#### Passing Parameters in C++ Delegates:

In Unreal, you can pass parameters to delegates by specifying the parameter types in the delegate definition.

```cpp
DECLARE_DELEGATE_ThreeParams(FTaskCompletedDelegate, FString, int32, float);

void ExecuteTaskWithParams(FTaskCompletedDelegate Delegate)
{
    // Simulate task completion
    Delegate.ExecuteIfBound(TEXT("Task Complete"), 200, 6.9f);
}
```

**Explanation**: The `DECLARE_DELEGATE_ThreeParams` macro allows you to pass parameters to the delegate when it is invoked, and you can pass multiple parameters as needed.

***

## Events vs. Callbacks

While both events and callbacks share similarities, they differ in their primary use cases.

* **Callback**: A function passed into another function as an argument, invoked after some processing is complete.
  * **Use Case**: Asynchronous tasks, such as handling I/O operations or animations.
* **Event**: An announcement raised by an object, to which other objects can listen and respond. Multiple listeners can subscribe to an event.
  * **Use Case**: Triggering responses to user input, gameplay events (e.g., an enemy being defeated), or other occurrences in the game world.

In Unreal Engine, events are typically implemented with delegates, while in Unity, the `UnityEvent` class or custom delegate-based events can be used to notify listeners.

***

## Conclusion

Callbacks and delegates are foundational concepts in game programming, enabling powerful, flexible, and efficient event-driven architectures. In Unity, C# delegates facilitate callbacks and event handling, while Unreal Engine’s C++ delegates and Blueprint exposure provide seamless integration with visual scripting. Understanding these patterns will allow you to build more dynamic, responsive game systems and enhance your workflow in both engines.

By embracing these concepts, you’ll improve the maintainability and scalability of your game’s code, allowing for cleaner and more modular design.
