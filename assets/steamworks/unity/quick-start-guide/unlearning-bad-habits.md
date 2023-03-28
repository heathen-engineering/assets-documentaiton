# Unlearning bad habits

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

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

The functionality that SteamManager provided in its original context is handled by Heathen's systems. Please see the [Steamworks Behaviour](../components/steamworks-behaviour.md) for a similar but quite different approach.
