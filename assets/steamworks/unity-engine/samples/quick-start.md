# Quick Start

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/concepts/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

This simple scene outlines the basic steps to get up and running with Steamworks.

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

This is a bare bones scene that does nothing more than initialize the Steam API. The key component in the scene is the [Steamworks Behaviour](../components/steamworks-behaviour.md) located on the Manager game object.

## Game Objects

### Manager

The manage game object has the [Steamworks Behaviour](../components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

## Components

### [Steamworks Behaviour](../components/steamworks-behaviour.md)

The Steamworks Behaviour is the component responsible for initializing and operating the Steam API integration. It is important that this is initialized as soon as possible in your game and is never destroyed or duplicated.

it is \*\***strongly\*\*** recommended to use a [bootstrap design pattern](../../../../company/concepts/design/bootstrap-scene.md) to insure that Steam API is initialized successful before even your main menu bothers to load.

### [Friend Profile](../prefabs/friend-profile.md)

![](<../../../../.gitbook/assets/image (2).png>)

The Friend Profile present in the scene is simply here to prove to you that the Steam API is initialized and able to read data. On load it will fetch the local user's data and populate the avatar image, name, status, friend ID and Steam level.
