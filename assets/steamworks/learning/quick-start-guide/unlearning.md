# Unlearning

## Introduction

Unfortunately there is a lot of just horrible sample and example code out their especially around Steamworks / Steam API. Here are some common things you might have picked up or learned that you should throw out right now.

### SteamManager.cs

This original came from an example on using the raw Steamworks.NET C# wrapper you can find the original at the link below

{% embed url="https://github.com/rlabrecque/Steamworks.NET-Example" %}

Keep in mind this was an example script, meant to be used with a specific example project and like any example script

{% hint style="danger" %}
Was never meant for production use
{% endhint %}

Sadly a great many Unity Asset developers do what Unity Asset developers often do and copy and pasted someone else's work into there own asset and ran with it without actually understanding what it was, why it was or how to do it properly.

{% hint style="info" %}
SteamManager should not be present much less used in any project
{% endhint %}

The functionality that SteamManager provided in its original context is handled by Heathen's systems. Please see the [Steamworks Behaviour](../../components/steamworks-behaviour.md) for a similar but quite different approach.
