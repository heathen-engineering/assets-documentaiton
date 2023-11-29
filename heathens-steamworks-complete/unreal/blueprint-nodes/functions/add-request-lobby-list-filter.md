---
cover: ../../../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 🔵 Add Request Lobby List Filter

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

When requesting a list of lobbies e.g. "searching" or "browsing" for lobbies, you must define the filter terms you wish to use before calling Request Lobby List to return the set of matching lobbies.

Steam provides several options for filtering and sorting the resulting lists as outlined below.

## Distance

Sets the physical distance for which we should search for lobbies, this is based on the users IP address and a IP location map on the Steam backed.

### Filter

The [UELobbyDistanceFilter](../enumerators/uelobbydistancefilter.md) option for lobby distance ... Default is the default 🤔

### Example

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Slots Available

Filters to only return lobbies with the specified number of open slots available.

### Slots Available

The number of open slots that must be open.

### Example

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Near Value

Sorts the results closest to the specified value.

Near filters don't actually filter out values, they just influence how the results are sorted. You can specify multiple near filters, with the first near filter influencing the most, and the last near filter influencing the least.

### Key

The filter key name to match.&#x20;

### Value to be Close To

The value that lobbies will be sorted on

### Example

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Numerical

Adds a numerical comparison filter

### Key

The filter key name to match.

### Value to Match

The numeric value to match

### Comparison Type

The [UELobbyComparison](../enumerators/uelobbycomparison.md) type to use for the assessment

### Example

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Result Count

Sets the maximum number of lobbies to return. The lower the count the faster it is to download the lobby results & details to the client.

{% hint style="info" %}
Valve limits this to a max, currently 50, Lobbies are not meant to be used as a discovery tool for every possible session running. Lobbies are meant for matchmaking. \
\
Ideally, you will search for the 1 top lobby that best matches your search arguments and join it.
{% endhint %}

### Max Results

The maximum number of lobbies to return. Steam will not return more than 50.

### Example

<figure><img src="../../../../.gitbook/assets/image (9) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## String

Adds a string comparison filter

### Key

The filter key name to match.

### Value to Match

The string value to match

### Comparison Type

The [UELobbyComparison](../enumerators/uelobbycomparison.md) type to use for the assessment

### Example

<figure><img src="../../../../.gitbook/assets/image (10) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
