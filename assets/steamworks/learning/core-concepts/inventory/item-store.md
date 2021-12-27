# Item Store

## Introduction

A common request we see is for an example in-game store or other "MTX" (micro-transcation) example.

Since Valve's Spacewar doesn't have a usable Steam Inventory configuraiton and since your store would be highly dependent on what items you have and how they are configured. The sample scene we have provided (9 Item Store Tutorial) simply contains example scripts based on this article and is meant to be a teaching tool not a funcitonal exmaple.

This article will discribe the concepts of an item store and cover several common use cases providing abstract examples for each. Finally at the end we will compile a list of commonly asked questions and of course if you have any questions please reach out to the community on our [Discord](https://discord.gg/6X3xrRc) server.

### Assumptions

This article assumes you have defined your items already. If you have questions about that see our [Getting Started](../../../features/inventory/getting-started.md) article.

This article also assumes you already understand how to create UI and behaviours in Unity. If you have questions there we strongly recomend you check out [this tutorial](https://learn.unity.com/pathway/junior-programmer). Its short and very useful for every Untiy developer.

## Creating UI

Creating the visuals is up to you, how you do it doesn't really matter and this subject is not impacted at all by Steam API you would do it the same way you would create any UI in your game.

As a common point of reference we assume your using Unity's uGUI&#x20;
