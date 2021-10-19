---
description: A quick start guide for those already comfortable with the basics.
---

# Quick Start Guide

## Steam Settings

Create a new Steam Settings object in your project folder by right clicking in your project tab and selecting\
**Create > Steamworks > Settings**

![Screen shot of a new empty Steam Settings object](<../../../.gitbook/assets/image (146).png>)

### Tips

The Steam Settings object is a Scriptable Object and contains all the configuration information for Steam's APIs. In most cases you will want to enable the **Conditional Compile** option by clicking the button at the top of the inspector. This will cause the system to recompile, with conditional compile enabled the system will strip out unusable portions of the API on build; that is for client builds the server APIs will be removed and for server builds the client APIs will be removed.

## App Id

Enter your app ID in the Application Id field

![Screen shot of the Application Id field of the Steam Settings object](<../../../.gitbook/assets/image (147).png>)

### Tips

Valve issues you an App ID when you pay your application fee. If you dont have your own ID yet you can use App ID 480 as a test ID. Heathe's samples and demos all use App ID 480.

## Steamworks Behaviour

Create a [Steamworks Behaviour](steamworks-behaviour.md) object in your [bootstrap scene](../../../company/concepts/bootstrap-scene.md) or similarly appropreate location; and drag your Steam Settings object into the provided field.

![Screen shot of a Steamworks Behaviour component](<../../../.gitbook/assets/image (19).png>)

Congratulations, you are now integrated with the Steam APIs. If you run the simulation, you will see that the Steam API initializes, and that the local user data object housed under the settings object populates with your Steam user information during play.

### Tips

[Steamworks Behaviour](steamworks-behaviour.md) should be initalized early in your application and never destroyed. It is keenly important that you do not reload the scene that defines the [Steamworks Behaviour](steamworks-behaviour.md) as this will cause issues with the Steam API.

If you need to reload the scene where [Steamworks Behaviour](steamworks-behaviour.md) is located or otherwise must use a singel scene architcture you should use the [Steamworks Creator](steamworks-creator.md) to insure the Steam API is managed correctly.

## Debugging

{% hint style="info" %}
You can visualize the internal state of the Steam API by opening the Steamworks Inspector while the simulation is running.
{% endhint %}

![Opening the inspector](<../../../.gitbook/assets/image (20).png>)

{% hint style="warning" %}
#### IMPORTANT

The inspector's Home and Lobbies tabs only populate while the simulation is running.
{% endhint %}

![Screen shot of the Steamworks Inspector while the simulation is running](<../../../.gitbook/assets/image (21).png>)

