# Inventory Settings

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../../../company/steam/">steam</a></td><td><a href="../../../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../../physkit/">physkit</a></td><td><a href="../../../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../../ux/">ux</a></td><td><a href="../../../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

accessed from within the SteamSettings.Client this houses inventory items and provides access to common values such as currency code and change events.

## Definition

```csharp
public class InventorySettings
```

## Fields and Attributes

### LocalCurrencyCode

```csharp
public Currency.Code LocalCurrencyCode => get;
```

Returns the currency code for the local user as reported by Steam.

### LocalCurrencySymbol

```csharp
public string LocalCurrencySymbol => get;
```

Returns the currency symbol (£, $, €, etc.) for the local user's configured currency.

### items

```csharp
public List<ItemDefinition> items;
```

The list of items configured for this app

## Events

### EventChanged

Triggered whenever the local user's inventory is updated from Steam.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(InventoryChangeRecord arg0)
{
}
```

Then you would register the event such as:

```csharp
SteamSettings.Client.inventory.EventChanged.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    SteamSettings.Client.inventory.EventChanged.RemoveListener(HandleEvent);
}
```

###
