---
cover: ../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
---

# Save Game

## Introduction

We have created a Steam Remote Storage Save Game class that extends Unreal's Save Game concept enabling it to work with Steam Remote Storage. You can use this as you would any typical Save Game in Unreal.

{% hint style="info" %}
Steam Remote Storage Save Game is derived from Unreal's Save Game class. As a result, it does everything a normal Save Game object would and can be used for traditional to-disk save operation if you so desire.\
\
We have simply provided additional functions that can be used to read and write the data to and from Steam's Remote Storage system.
{% endhint %}

{% hint style="info" %}
Steam Remote Storage aka Steam Cloud Save\
Is a drop box-like file sync system that synchronizes files written to the local disk to Steam's remote storage (aka cloud). It does work in offline mode and handles syncing data between all devices the user plays on.
{% endhint %}

## Setup

Start by creating a blueprint class and here we will choose the Steam Remote Storage Save Game as our base class.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Next, add whatever variables you would like to have saved.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

And that is all that is required to create your Save Game object. Creating, setting and reading values from the Save Game object is the same as you would use with any Unreal Save Game object.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p>Assume Test Save Game is my Blueprint derived from Steam Remote Storage Save Game</p></figcaption></figure>

## Write File

To save the file to Steam Remote Storage you will use the Steam Write File and Steam Write File Async Blueprint functions

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Synchronious File Write</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Asynchronious File Write</p></figcaption></figure>

## Read File

To read the file from Steam Remote Storage you will use the Steam Read File and Steam Read File Sync Blueprint functions

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption><p>Synchronious File Read</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Asynchronious File Read</p></figcaption></figure>
