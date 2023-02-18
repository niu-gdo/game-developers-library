# Create a New Unity Project
By Jake Rogers

## Introduction
After [installing Unity](./unity-first-step-install.md), we can create a new project through Unity Hub. In this series, we will be creating a project in the vein of Unity's iconic newbie project: *Roll-a-Ball*!

## Project Creation Menu
In Unity Hub, click 'New Project' from the 'Projects' tab.

At the top, you can select your installed editor version in case you have multiple installations. Pick the most recent LTS version.

Unity comes with some templates for new projects you can select, each one giving you a clean slate or jumping-off-point for prototyping a particular type of game.

### (ℹ) Project Type Capabilities
Unity, like other populat game engines, has support for making many types of games. Here are some brief notes about Unity's ability to make certain types of games.

* **3-D**: 3D has been supported in Unity since its 1.0 release all the way back in 2005! Arguably being a specialty amongst the other game types, you will find no lack of support here. Unity has been used in many high-profile 3D games, such as Escape From Tarkov, Rust, and Risk of Rain 2.

* **2-D**: 2D in Unity has gotten some flak in the past for not being as intuitive as 3D. In fact, you will find that Unity's 2D most is obstensibly a 3D game loosely constrained to a single plane. Certain workflow tools for things like tilemapping are not as sophisticated as they are in other 2D capable engines.  
However, most of these concerns come from older posts and threads, as Unity's 2D has come a long way and is very functional. In fact, many of the most popular 2D games are made with Unity, such as RimWorld, Hollow Knight, and Cuphead.

* **Augmented Reality (AR)**: Unity is a very popular choice for Augmented Reality software, where virtual game elements are projected on top of the physical world. [Read More](https://unity.com/unity/features/ar)

* **Virtual Reality (VR)**: Many of the most popular VR games are made with Unity, such as VRChat, Blade & Sorcery, Beat Saber, and BONEWORKS.

### (ℹ) Scriptable Render Pipelines
When picking a project template, you will notice that there are multiple different types of the same template:

* 3D
* 3D (URP)
* 3D (HDRP)
* 2D
* 2D (URP)

The difference here is the type of **Scriptable Render Pipeline (SRP)** being used. SRPs allow for Unity to provide multiple different ways for projects to handle rendering graphics from the game to screens. Each choice render pipeline has some different features.

* **Default (Built-In Renderer)**: With no pipeline specified, Unity defaults to the *Built-in Renderer*. This is what Unity used before SRPs were rolled out in around 2019. While it is general-purpose, it has limited customization options.
* **Universial Render Pipeline (URP)**: The URP is an easy to customize, performant render pipeline designed for a large range of target platforms, from low-end mobiles to PCs. This makes URP a good choice for games with low or medium graphical fidelity, though one can still create very impressive scenes with it.
    * For a brief time, URP was formerly known as the *Light-Weight Render Pipeline*, or (LWRP).
* **High-Definition Render Pipeline (HDRP)**: The HDRP is designed to produce AAA quality graphics specifically targeted as high-end platforms, making it a good choice for games trying to have cutting-edge graphics.

The Built-In Renderer, URP, and HDRP are available for 3D games, while 2D only has the Built-In Renderer and URP.  

**In most cases, you will want to go for the Universial Render Pipeline for your projects**. You likely will not have assets to high-fidelity assets to make the cutting edge rendering worth it, and you may find it has a heavier load on your editor.

The Built-In Render is arguably superceded by the URP. Developers report getting better frame-rates with URP while having easier customization options and better fidelity. 2D URP games also get access to optimized, slick 2D lighting options.

### Pick a Template
For our *Roll-a-Ball* game, we will simply pick the 3D (URP) template.

On the right side, pick a name for your project. *Roll-a-Ball* works, or give it your own name if you feel that is creatively bankrupt.

You can also pick a directory for your project. I recommend changing it to a fast drive on your system, such as an SSD or M.2 drive. [Unity has a reputation for being quite hefty to load](https://i.redd.it/sqa3vpmcv4t61.jpg).

When you're ready, press 'Create Project' and your project will be initialized for you. The first load will take a little bit longer than subsequent loads.

## Conclusion
You now have a new playground to mess around in, time to get to work! \o/

Next: [Unity Editor Basics]()