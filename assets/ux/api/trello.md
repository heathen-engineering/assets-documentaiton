---
description: Read and write Trello cards
---

# Trello

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../steam/steam.md">steam.md</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../learning/core-concepts/">User eXperience Tools</a></td><td><a href="../learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## IntroductionIntroduction

```csharp
public static class API.Trello
```

A simple Trello interface enabling access to Trello cards.

### What can it do?

This can be used to create Trello cards on a target board in a target list. You can upload attachments to the card including images, files, etc.

This interface requires a valid API key and token to be used. For more information please see the Trello API site

{% embed url="https://trello.com/app-key" %}

## How To

{% hint style="warning" %}
All operations require a valid Trello API key and token.

In most cases you will not want to ship a game with Trello integration active however it can be very useful during development with development builds or in limited testing situations.

As an alternative to Trello you may want to consider Unity's User Reporting feature which is more appropreat to be used on produciton clients.

[https://unitytech.github.io/clouddiagnostics/userreporting/UnityCloudDiagnosticsUserReports.html](https://unitytech.github.io/clouddiagnostics/userreporting/UnityCloudDiagnosticsUserReports.html)
{% endhint %}

### Get a list of available boards

Get a list of available boards, you would typically do this to get a board ID for use in the GetLists operation.

```csharp
StartCoroutine(API.Trello.GetBoards(key, token, callback));
```

### Get a list of list objects

Get a list of lists in this board, you would typcially do this to get a list of lists available to this board for use in the GetCards or CreateCard operations.

```csharp
StartCoroutine(API.Trello.GetLists(key, token, boardId, callback));
```

### Get Cards

Get a list of cards in the indicated list.

```csharp
StartCoroutine(API.Trello.GetCards(key, token, listId, callback));
```

### Create Card

Create a new card and optionally attach local files to it.

```csharp
StartCouroutine(API.Trello.CreateCard(key,
                                      token,
                                      listId,
                                      cardName,
                                      cardDescription,
                                      attachments,
                                      callback));
```

{% hint style="info" %}
The attachments should be a collection of fully qualified paths to the files to be attached to the card.
{% endhint %}
