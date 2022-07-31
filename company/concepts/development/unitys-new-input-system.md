# Unity's "New" Input System

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

This article will walk through the steps to enable and Disable the new Input System and the common troubleshooting issues

## Enable

### Step 1

Install the new input system from the Package Manager. You should do this before you change your project settings.

{% hint style="info" %}
NOTE

Doing this (installing the Input System) should cause Unity to toggle the New Input System on for you so you can usually skip Step 2.
{% endhint %}

![](<../../../.gitbook/assets/image (186).png>)

### Step 2

Enable the new input system in your project settings.

{% hint style="info" %}
NOTE

Usually Unity will do this for you when you install the Input System as done in Step 1 so this should already be done for you.
{% endhint %}

![](<../../../.gitbook/assets/image (167) (1) (1) (1) (1) (1) (1) (1).png>)

## Disable

### Step 1

Remove the Input System from the Package Manager ... we like to do this first even though it may throw a compiler errors for assets that use both new and old; we find it faster/nicer to remove it before toggling the setting as the setting will force a restart.

![](<../../../.gitbook/assets/image (185).png>)

As noted this will cause two exceptions or more to be thrown ... this is expected and will be resolved in the next step.

![](<../../../.gitbook/assets/image (163) (1) (1) (1).png>)

This happens because your settings still say to use the New Input System ... but you dont have the New Input System installed.

### Step 2

Toggle your Player Settings to use the "Old" Input System.&#x20;

{% hint style="info" %}
NOTE

This will restart Unity
{% endhint %}

![](<../../../.gitbook/assets/image (166) (1) (1).png>)

