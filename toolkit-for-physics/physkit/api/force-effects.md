# Force Effects

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public static class ForceEffects
```

Found in namespace:

```csharp
using HeathenEngineering.UnityPhysics.API;
```

### What can it do?

Used primarily by Force Effect Fields and Receivers this API manages global effects and is not intended for use by the developer.

## Global

You can access the active set of global effect sources via

```csharp
API.ForceEffects.Global;
```

This is a List of ForceEffectSources that are currently active, ForceEffectSources add and remove them selves from this when enabled / disabled.
