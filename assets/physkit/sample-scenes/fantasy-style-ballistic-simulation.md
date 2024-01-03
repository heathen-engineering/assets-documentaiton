# Fantasy Style Ballistic Simulation

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

![](<../../../.gitbook/assets/image (180) (1) (1) (1) (1).png>)

This scene demonstrates the use of the Ballistics API to solve form a desired trajectory and to then apply that result to a physically simulated projectile.

In this example we make use of the Ballistics.Solution method that allows us to stylize the trajectory by dictating the arc height and ground speed the projectile will take. UI sliders are made available which will adjust these settings per shooter to help you visualize the effect.

## What do I Learn?

1. How to access the Ballistics API from your scripts
2. How to apply Solution results to projectiles
3. How to stylize trajectory to meet your games visual needs while remaining 100% physically simulated using standard Rigidybody components.

## Objects

### Arrow

You will find the Arrow GameObject in the Stylized Shot > Templates GameObject. This is the projectile that is being fired by the 4 shooters and uses the `Sample1FantaasyProjectile` to help apply the required physical properties to the projectile.

```csharp
public class Sample1FantasyProjectile : MonoBehaviour
```

{% hint style="danger" %}
As with all example scripts; this script has been written to be easy to read for learning purposes. It has not been coded to be efficient. \
\
For example you should generally avoid using the .transform field on Rigidbody or GameObject as this must perform a GetComponenet call every time its used. We use it here to make it very clear what transform we are operating on and because performance is not relevant for this demo.
{% endhint %}

On start this script grabs a reference to the attached Rigidbody and sets the drag and angular drag to 0, turns off gravity simulation and sets the velocity to the calculated value.

We turn off gravity when using this particular type of solution because we want to apply a custom gravity force who's strength is unique to this projectile. This is what allows us to assign the ground speed and height the projectile will take.

You will see that in the Fixed Update we apply our custom gravity accounting for the projectiles mass and then we rotate the projectile to face along the velocity direction.

## Demo Script

The DEMO SCRIPTS object implements the Sample 1 Ballistic Basics script and is what drives the process of UI and triggers the shooting.

In this case you will see that we define a "shooter" as a start position and target position represented by Transforms and we connect directly to UI sliders to control the max height and linear  speed for each shooter.

The Update method of the script simply checks time and if ready calls the "Shoot" method.

The Shoot method is what calls the Ballistics API to get a firing solution given the provided inputs for this shooter. If a solution is found it will spawn a projectile and assign the solution results (Velocity and Gravity in this case).
