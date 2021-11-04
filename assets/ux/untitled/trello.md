---
description: Read and write Trello cards
---

# Trello

## Introduction

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
