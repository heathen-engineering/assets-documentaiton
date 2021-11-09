# Downloadable Content Object

## Definition

```csharp
public class DownloadableContentObject : ScriptableObject
```

Represents a DLC object, this is created by the [Steam Settings](steam-settings.md) object when you import DLC data for your app. To learn more see the [Steam Settings](steam-settings.md) object documentation.

### Fields and Attributes

| Type     | Name         | Comment                                            |
| -------- | ------------ | -------------------------------------------------- |
| AppId\_t | appId        | The room this message relates to                   |
| bool     | IsSubscribed | Indicates rather or not the DLC is currently owned |
| bool     | IsInstalled  | Indicated rather or not the DLC is installed       |

### Methods

```csharp
public string GetInstallDirectory();
```

Returns the intall location of the DLC

```csharp
public float GetDownloadProgress();
```

Returns the download progress if known as a value between 0 and 1

```csharp
public DateTime GetEarliestPurchaseTime();
```

Gets the time of purchase if known

```csharp
public void Install();
```

Starts the process of installing the DLC

```csharp
public void Uninstall();
```

Starts the process of uninstalling the DLC

```csharp
public void OpenStore(flag);
```

Opens the Steam Overlay to the Store for this DLC item
