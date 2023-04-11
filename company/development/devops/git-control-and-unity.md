---
description: Take control of your project
---

# 🛂 Git Control & Unity

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../steam/">Guides and Tutorials</a></td><td><a href="../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks_Cover.jpg">Steamworks_Cover.jpg</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../assets/physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../assets/physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../assets/ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

{% hint style="warning" %}
You generally do not want your Unity Project to be the root of your repository.\
\
Read our example and its steps and understand why.\
\
You do want your repository to have a folder with in it that will be your Unity Project root. This simplifies other aspects later ... read on to better understand.
{% endhint %}

The concept of source control is critically important for game development. The idea is simply that not only is your source code "backed up" but every change made to your source is tracked and managed and can be reviewed, compared or even rolled back.

In times past you would have needed a paid service such as Perforce, Plastic SCM, Team Foundation or similar. These premium tools do still exist and are a fine option, however several free options are also available. Git or more specifically GitHub has become increasingly friendly to use, integrates with many build services such as Unity Cloud Build and has free levels of use.

This article will describe the steps required to set up a new repository for use with Unity and discus the integration Git has with Visual Studio and other tools.

## Git Organization

Before we do anything lets talk about how you log into GitHub and how you manage your Git repositories.

If your building a game you either are now or very likely will soon be working with others. Even if you never plan to work with others you very likely want to have a separate life from your game development work. For that reason I do suggest you create a Git Organization and that its under the organization that you create your game development repositories.

Creating an organization isn't hard, its free and you can convert personal accounts into organizations if you should need.

{% embed url="https://github.com/settings/organizations" %}

## Installing GitHub Desktop

While not technically required if your new to Git or just not a fan of command line tools, GitHub Desktop is a free and easy way of managing your repositories. This tool will help you connect to repositories, download repositories, and push changes to repositories from a simple desktop app.

{% embed url="https://desktop.github.com/" %}

## Creating a Repository

Your first step should be to create your repository, I prefer to do this from the Git Website so I show those steps here.

### Step 1&#x20;

Navigate to your organization's home page. This is usually just gethub.com followed by your organization name. For example this is the URL for Heathen Engineering's organization

{% embed url="https://github.com/heathen-engineering" %}

### Step 2

As the owner of an organization you will see a simple green button near the top ladled "New"; click that.

![](<../../../.gitbook/assets/image (183).png>)

### Step 3

Name your repository something clever ... remember this wont be the name or folder that appears in Unity Hub. This will be the parent folder with in which your Unity Project and any other control artefacts will reside.

Heathen usually names this for the projects code name, not the game's name its self; you'll see why shortly

{% hint style="success" %}
Be sure to set the `Add .gitignore` field to `Unity` this will give you a handy ignore file to stop Unity from bloating your repository with generated files.
{% endhint %}

![](<../../../.gitbook/assets/image (158).png>)

### Step 4

Open your repository In GitHub Desktop by pressing the Green button and selecting `Open with GitHub Desktop`

![](<../../../.gitbook/assets/image (170).png>)

Follow the on screen instructions which are simply having you select a location on your local disk to put the repository.

![](<../../../.gitbook/assets/image (159).png>)

and click `Show in Explorer`

![](<../../../.gitbook/assets/image (171) (1).png>)

Copy the folder path, you will need it for the next step

### Step 5

Now we create the Unity Project.&#x20;

Open Unity Hub and click new project as you normally would, select your engine version and template if you like. Then select the folder where the project should be placed and paste in the folder path we copied from Step 4 above.

![](<../../../.gitbook/assets/image (182).png>)

### Step 6

Now that we have our clean project set up we need to move the .gitignore file into it so it doesn't make a huge mess when we first check in.

To do this, open the project folder and navigate up one till you see the .gitignore file

![](<../../../.gitbook/assets/image (167).png>)

We want to move this into the Unity Project folder, so in my case I would simply drag and drop it in the `A Game` folder.

### Step 7

With that we are done!

![](<../../../.gitbook/assets/image (180).png>)

You can pop back over to GitHub Desktop and see that it has detected all the changes made by adding the Unity Project.

All that is left to do is to add a summary and description to the change and commit to main, using the text box in the lower left corner of the GitHub Desktop screen.

{% hint style="warning" %}
Don't for get to click the `Push origin` button after committing.

\
GitHub works in two stages, commit and then push.
{% endhint %}

Once complete you can see that your changes appear in the repositor as seen on the web

![](<../../../.gitbook/assets/image (184).png>)

## Tips

You will notice that the game project folder is a child of the repository. Meaning we can add other files and folders out side the project here.

That could be simple documentation, concept documents and artwork or even other Unity Projects as you experiment with your game design.

This repository represents your game project not just the specific Unity Project your working in at the moment.

## Visual Studio

Did you know Microsoft owns Git?

Well now you do, and they build Visual Studio, the default and hands down best IDE for working with Unity ... in my opinion anyway.

Visual Studio will detect that this project is part of a Git repository and will let you work with Git right in your IDE so really you don't require GitHub Desktop but its nice if you want to control more than just your scripts.

![](<../../../.gitbook/assets/image (168).png>)

