# 🎮 Unity Engine

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

The articles within are specific to Unity and include the engine specific tools and systems unique to the Unity version of the package.&#x20;

The Heathen [APIs](../api/) and [Objects](../objects/) being native C# are \*\***nearly\*\*** identical between Unity and Godot with the only difference being the use of each engines native structures ...&#x20;

for example&#x20;

in Unity:

```csharp
public void LoadAvatar(Action<Texture2D> callback)
```

in Godot:

```csharp
public void LoadAvatar(Action<Image> callback)
```
