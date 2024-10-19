# Constant Acceleration

{% hint style="success" %}
#### Like what you are seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The Constant Acceleration tool is available for TrickShot, TrickShot2D and BallisticAim. The purpose of the tool is to calculate the acceleration that will be applied to a projectile in flight given the provided inputs.

This component can account for both global and local effects. If your use case only requires global effects such as Gravity and Coriolis then you can skip using this component and simply enter the sum of the effects in the Constant Acceleration field of the TrickShot, TrickShot2D or BallisticAim components.

This component comes into use when you want to apply local effects as well such a Magnus effect which is generally calculated relative to the emitter.

## Effects

in the above, we talk about multiple effects that can be applied to a projectile in flight. For most games and most use cases, the only effect you need to worry about is the effect of gravity. Earth's gravity is aprox (0, -9.81, 0) and is the default value you will see applied to the TrickShot, TrickShot2D and BallisticAim components.

If you are only using gravity, you do not need this component.

{% hint style="info" %}
You are making a video game, you do not have to emulate reality, be creative and play with global and local effects to produce interesting yet predictable trajectories
{% endhint %}

### Global Effects

These are effects whose directional influence is global to the game world e.g. Gravity and Coriolis are both global&#x20;

#### Gravity

Should need no introduction, this is the effect a mass applies to another mass and draws them together. Practically speaking the planet you are on applies an effect we express as a constant acceleration toward its centre. Since most games are not spherical we can simply express this as a constant toward acceleration.

#### Coriolis

An effect applied by the spinning of the relative body ... e.g. because the earth is spinning a projectile in free flight will tend to drift west, owing to the Earth spinning toward the East. For most use cases this effect is far too small to be relevant however if you're doing a sniper or artillery game where distances and or tolerance are very small this may be of more relevance.

### Local Effects

This is the main use for the component, the application of localized effects, meaning effects that are applied relative to the rotation of the emitter. The most common example of this is the Magnus effect.

#### Magnus

The precession a spinning object experiences in flight e.g. the "curve ball" effect. This value is generally calculated relative to the emitter, so for example, you might spin the ball to hook to the right, which means it will hook to the right as observed by the emitter.&#x20;

Most projectile systems such as a gun or cannon are "rifled" (spin on the axis of traverse) to stabilise thus making this effect insignificant. Where this becomes more relevant is sports and science simulations where the projectile such as a golf ball, tennis ball or baseball is given a spin to induce a hook (curve)

## Namespace

```csharp
namespace HeathenEngineering.UnityPhysics;
```

## Definition

Available for 3D Physics

```csharp
public class TrickShotLine : MonoBehaviour
```

And for 2D Physics

```csharp
public class TrickShotLine2D : MonoBehaviour
```

## Fields and Attributes

### Run On Start

```csharp
public bool runOnStart;
```

If true the line will be updated when the Start method is called by Unity.

### Continuous Run

```csharp
public bool continuousRun;
```

If true the component will update the line every frame calling the [Trick Shot Perdict](trick-shot.md#predict) method each frame.

