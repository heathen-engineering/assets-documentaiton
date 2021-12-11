# Force Effects

## Introduction

```csharp
public static class ForceEffects
```

Found in namespace:

```csharp
using HeathenEngineering.PhysKit.API;
```

### What can it do?

Used primarly by Force Effect Fields and Recievers this API manages global effects and is not intended for use by the developer.

## Global

You can access the active set of global effect sources via

```csharp
API.ForceEffects.Global;
```

This is a List of ForceEffectSources that are currently active, ForceEffectSources add and remove them selves from this when enabled / disabled.
