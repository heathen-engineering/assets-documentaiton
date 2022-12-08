# Currency

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public static class Currency
```

A simple class used to list the supported currency codes available in Steam and to fetch the string symbole of those codes.

```csharp
public enum Currency.Code
```

A simple enum which lists all of the supported currency codes available in Steam

## Methods

### GetSymbole

```csharp
public static string GetSymbole(Currency.Code code);
```

Returns the string symbole used by this currency e.g. £, $, € etc.
