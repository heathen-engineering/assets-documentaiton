# DevOps

## TL;DR Just the Basics - Source Control

The concept of source control is critically important for game development. The idea is simply that not only is your source code "backed up," but every change made to your source is tracked and managed and can be reviewed, compared or even rolled back.

In times past you would have needed a paid service such as Perforce, Plastic SCM, Team Foundation or similar. These premium tools do still exist and are a fine option, however, several free options are also available. Git or more specifically GitHub has become increasingly friendly to use, integrates with many build services and has free levels of use.

This article will describe the steps required to set up a new repository for use with Unity and discuss the integration Git has with Visual Studio and other tools.

### Git Organization <a href="#git-organization" id="git-organization"></a>

Before we do anything let's talk about how you log into GitHub and how you manage your Git repositories.

If you are building a game, you either are now or very likely will soon be working with others. Even if you never plan to work with others, you very likely want to have a separate life from your game development work. For that reason, I suggest you create a Git Organization and that it's under the organization that you create your game development repositories.

Creating an organization isn't hard; it's free, and you can convert personal accounts into organizations if you need them.

{% embed url="https://github.com/settings/organizations" %}

### Installing GitHub Desktop <a href="#installing-github-desktop" id="installing-github-desktop"></a>

While not technically required if you are new to Git or just not a fan of command-line tools, GitHub Desktop is a free and easy way of managing your repositories. This tool will help you connect to repositories, download repositories, and push changes to repositories from a simple desktop app.

{% embed url="https://desktop.github.com/" %}

### Creating a Repository <a href="#creating-a-repository" id="creating-a-repository"></a>

Your first step should be to create your repository. I prefer to do this from the Git Website so I show those steps here.

#### Step 1 <a href="#step-1" id="step-1"></a>

Navigate to your organization's home page. This is usually just gethub.com followed by your organization's name. For example, this is the URL for Heathen Engineering's organization

{% embed url="https://github.com/heathen-engineering" %}

#### Step 2 <a href="#step-2" id="step-2"></a>

As the owner of an organization, you will see a simple green button near the top labelled "New"; click that.

{% hint style="warning" %}
Be sure your repo is "Private" especially if you will have 3rd party code in your repo. Otherwise, you could leak your code and the code you licensed from others.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

#### Step 3 <a href="#step-3" id="step-3"></a>

Name your repository something clever ... remember this won't be the name or folder that appears in Unity Hub. This will be the parent folder within which your Unity Project and any other control artefacts will reside.

Heathen usually names this for the project code name, not the game's name itself; you'll see why shortly

{% hint style="success" %}
Be sure to set the `Add .gitignore` field to `Unity` or `Unreal` Or whatever tool you are using, this will give you a handy ignore file to stop Unity from bloating your repository with generated files.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### Step 4 <a href="#step-4" id="step-4"></a>

Open your repository in GitHub Desktop by pressing the Green button and selecting `Open with GitHub Desktop`

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Follow the on-screen instructions, which simply have you select a location on your local disk to put the repository.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

and click `Show in Explorer`

Copy the folder path, you will need it for the next step

#### Step 5 <a href="#step-5" id="step-5"></a>

Now we create the Unity, Unreal, Godot, etc Project.

Open Unity Hub or Launcher, click New Project as you normally would, then select the folder where the project should be placed and paste it into the folder path we copied from Step 4 above.

{% hint style="info" %}
It's generally recommended to put the editor project in a folder under the repository's root, such as\
\
root/UnrealProject/MyGameProjectFolder\
\
This is handy as it gives you room to place other folders in source control that are not siblings or children of the project root, such as ThirdParties, Art Source, Models, Documentation, etc.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

#### Step 6 <a href="#step-6" id="step-6"></a>

Now that we have our clean project set up, we need to move the .gitignore file into it so it doesn't make a huge mess when we first check in.

To do this, open the project folder and navigate up one till you see the .gitignore file

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

We want to move this into the Unity Project folder, so in my case, I would simply drag and drop it in the `A Game` folder or whatever you named your Game Project folder ... it should be in the root of your game project so right next to your solution file, Asset folder, etc.

#### Step 7 <a href="#step-7" id="step-7"></a>

With that, we are done!

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

You can pop back over to GitHub Desktop and see that it has detected all the changes made by adding the Unity Project.

All that is left to do is to add a summary and description to the change and commit to the main, using the text box in the lower-left corner of the GitHub Desktop screen.

## Visual Studio <a href="#visual-studio" id="visual-studio"></a>

Did you know Microsoft owns Git?

Well, now you do, and they build Visual Studio, the default and hands-down best IDE for working with Unity, Unreal or most programming solutions ... in my opinion anyway.

Visual Studio will detect that this project is part of a Git repository and will let you work with Git right in your IDE, so really, you don't require GitHub Desktop, but it's nice if you want to control more than just your scripts.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

## Deep Dive into DevOps

**DevOps**, short for **Development Operations**, refers to the set of practices, tools, and cultural philosophies designed to streamline and improve the development, deployment, and maintenance of software. In the context of game development, DevOps focuses on enhancing the collaboration between development teams and operations teams, ensuring that games are built, tested, and released smoothly, efficiently, and consistently.

At a fundamental level, DevOps ensures that developers have the tools and practices in place to effectively manage their code, build pipelines, automate testing, and deploy games to players. While the scope of DevOps can vary depending on the size of the project, even small indie teams can benefit greatly from adopting its core principles. At a minimum, DevOps in game development includes:

* **Source Control**: This is the backbone of any development process. Tools like Git (with platforms like GitHub, GitLab, and Bitbucket) enable teams to track and manage changes to their game’s codebase. Source control helps developers work on the same codebase without overwriting each other’s work, and it enables easy collaboration and versioning.
* **Change Management**: This refers to managing and tracking changes in code and assets. It’s about having a clear understanding of what changes have been made, by whom, and when. This is often achieved through a combination of source control, pull requests, and detailed commit messages.
* **Build Automation**: As you develop your game, you will constantly be compiling and testing your code. Automating the build process is key to saving time and avoiding human error. Tools like Jenkins, Unity Cloud Build, or Azure DevOps can automatically compile your game and run tests whenever changes are made to the codebase, ensuring everything is working as expected.
* **Automated Testing**: In game development, testing is crucial. Automated tests ensure that new code does not break existing functionality. These can be unit tests for individual pieces of code or integration tests to ensure that different systems in your game work together seamlessly. Unit testing frameworks like NUnit (C#) or Google Test (C++) can be integrated into your build pipeline to automatically run tests after each change.

With the vast number of tools available to modern game development teams, ranging from **free services** like GitHub and Unity Cloud Build to more specialized third-party tools like **Perforce** or **Plastic SCM** (which are widely used in larger studios), there’s no shortage of options for managing DevOps workflows. Additionally, industry-standard solutions like **Azure DevOps** can provide a comprehensive suite of tools for source control, CI/CD (Continuous Integration/Continuous Deployment), project management, and more, offering a full-featured pipeline for studios of all sizes.

***

## Learning DevOps - A Game Developer’s Journey

**DevOps** is a broad field, and mastering it can take years of experience, often forming a career path on its own. It involves understanding not only the tools used but also the philosophies and practices that guide the management and delivery of software across its entire lifecycle. As a game developer, you don’t need to be a DevOps expert to benefit from it, but understanding its key concepts will significantly improve how you approach development, testing, and deployment.

However, it’s important to understand that DevOps is just one piece of a much larger puzzle, which in the software industry is often referred to as **Application Lifecycle Management (ALM)**. ALM encompasses everything from project planning and source control to testing, deployment, and even monitoring post-launch. For most hobbyists and indie developers, the more complex and technical aspects of DevOps and ALM may not be necessary, but it’s still essential to grasp the basics of these concepts to maintain a healthy, sustainable development process.

At the core, **DevOps** provides practices that make the development process more predictable and scalable. In game development, this is particularly important because of the unique nature of the medium: the combination of large codebases, media assets (art, sound, etc.), and complex runtime systems. For smaller teams, setting up proper DevOps pipelines can drastically improve workflow efficiency and reduce headaches down the line. Even for solo developers or small teams, having source control, automated testing, and a build pipeline set up early on can save significant time, especially as the project grows in size and complexity.

If you want to dive deeper into DevOps and ALM, a good place to start is with **Microsoft’s documentation and learning resources**. Microsoft offers a variety of free courses, tutorials, and tools for DevOps, making them an excellent entry point for anyone, regardless of the game engine you use. Their platform, **Azure DevOps**, integrates well with both Unity and Unreal Engine and offers many services that streamline the development process, from build automation to testing and deployment.

While it’s tempting to skip over the details and jump straight into coding, understanding and implementing DevOps early on will pay off in the long term. By setting up a robust pipeline for managing code, assets, and testing, you can focus more on developing your game and less on troubleshooting bugs caused by poorly managed builds.

#### Tools to Get You Started

Here are some tools that can help you get started with DevOps in game development:

* **GitHub**: A free, widely used platform for source control that integrates well with Unity. It offers both Git and GitHub Actions, which can help you automate build and deployment processes.
* **GitLab**: Another great option for source control, and it provides built-in CI/CD capabilities for automating your build, test, and deployment pipeline.
* **Unity Cloud Build**: A tool built specifically for Unity game developers that automates the process of building and testing your game on multiple platforms. It also integrates well with GitHub.
* **Azure DevOps**: A complete suite of DevOps tools that includes source control, build automation, testing, and deployment pipelines. This is an excellent solution if you're working on a larger project or need more integrated functionality.
* **Perforce/Plastic SCM**: If you’re working on large teams with significant assets (like in AAA games), these tools are known for handling large binary files and complex asset management much better than Git.
