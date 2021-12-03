# Input Action Data

## Definition

```csharp
public struct InputActionData;
```

## Fields and Attributes

| Type             | Name       | Comment                                                                                              |
| ---------------- | ---------- | ---------------------------------------------------------------------------------------------------- |
| InputHandle\_t   | controller | The controller this action data was read from                                                        |
| InputActionType  | type       | Analog or Digital                                                                                    |
| bool             | active     | Is this action active e.g. part of an active set or layer                                            |
| EInputSourceMode | mode       | Only used for analog actions, indicates the type of analog action simulated e.g. mouse, stick, etc.. |
| bool             | state      | True if this action is active. For analog actions this is true if either x or y is non-zero          |
| float            | x          | For analog actions this indicates the x axis                                                         |
| float            | y          | For analog actions this indicates the y axis                                                         |

