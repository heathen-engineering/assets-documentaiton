---
description: >-
  A picture is worth a thousand words and about 500 lines of code ... this lets
  you do it in 1
---

# Screenshot

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../learning/core-concepts/">User eXperience Tools</a></td><td><a href="../learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public static class API.Screenshot
```

This interface enables you to capture full screen or parts of a screen to texture, to file and to optionally scale the data to suit your needs.

### What can it do?

* Capture full screen to texture
* Capture a rect of the screen to texture
* Scale a texture (point or bilinear)
* save a texture or the screen or part of the screen to disk

## How To

{% hint style="info" %}
All processes are asynchronious and require you to pass in a MoboBehaviour so that the interface can detect the end of frame insuring a proper capture of the redering.



Once complete the callback will be invoked providing you with the completed texture and a boolean indicating IO Failure if any for example



```csharp
API.Screenshot.Capture(this, (texture, failure) => 
{
    if(!failure)
        Debug.Log("texture contains the screen shot!");
});
```
{% endhint %}

### Capture the full screen

```csharp
API.Screenshot.Capture(component, callback);
```

### Capture part of the screen

From repreesnts the lower left and To represents the upper rigth of the corners of the screen rect to be taken, these are in pixel space e.g. (0,0) & (256,256) would capture a 256x256 area at the botton left corner of the screen.

```csharp
API.Screenshot.Capture(componenet, from, to, callback);
```

### Save image to file

You can capture and save in a single line call to any of Unity's supported encoding types. The save image operation can also be used on Texture2D so you can save any texture you have available.

```csharp
API.Screenshot.SaveImage(componenet,
                         path,
                         imageType,
                         scaleToResoltuion,
                         lowerLeftCorner,
                         upperRightCorner,
                         callback);
```

All paramiters except the componenet paramiter are optional, that is you could capture a screen shot with as little code as

```csharp
API.Screenshot.SaveImage(componenet);
```

The result is that the full screen would be captured at full resolution and saved to the game's persistant data storage path as a JPG with the name `screenshot_20210113133230.jpg` note the format of the file name is simply `screenshot` followed by the current date time in the form `yyyyMMddHHmmss` this should insure the file does not overwrite unless you managed to call this method twice within one second.

In most use cases you actually want to save a scaled down version of the screenshot such as for a thumbnail in a save file. To do that you would use

```csharp
API.Screenshot.SaveImage(componenet,
                         path,
                         default,
                         new Vector2Int(256, 144),
                         default,
                         default,
                         callback);
```

By passing default in we ask the method to use its defaults e.g. JPG and to capture the full screen. In this example we chose to speicify the path, resolution and a callback. The callback will give us the texture 2D so we can show it to screen for the user, it will also tell us the final path that was saved to and rather or not there where any IO errors.

### Scale a texture

The screenshot interfaces Point and Bilinear scale operations are exposed for your use, this can be useful when creating other thumbnail like images. There use is simple and strait forward

```csharp
API.Screenshot.BiliniearScale(texture, width, height);
```

The texture will be resized with its contnet adjusted to scale into the width and height provided.
