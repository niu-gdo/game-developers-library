# Scriptable Render Pipelines
*By Jake Rogers*

## Renderers
When picking a project template, you will notice that there are multiple different types of the same template:

* 3D
* 3D (URP)
* 3D (HDRP)
* 2D
* 2D (URP)

The difference here is the type of **Scriptable Render Pipeline (SRP)** being used. SRPs allow for Unity to provide multiple different ways for projects to handle rendering graphics from the game to screens. Each choice render pipeline has some different features.

* **Default (Built-In Renderer)**: With no pipeline specified, Unity defaults to the *Built-in Renderer*. This is what Unity used before SRPs were rolled out in around 2019. While it is general-purpose, it has limited customization options.
    * Note that the Built-In Renderer is **not** a SRP; it is a legacy renderer from before SRPs were introduced.
* **Universial Render Pipeline (URP)**: The URP is an easy to customize, performant render pipeline designed for a large range of target platforms, from low-end mobiles to PCs. This makes URP a good choice for games with low or medium graphical fidelity, though one can still create very impressive scenes with it.
    * For a brief time, URP was formerly known as the *Light-Weight Render Pipeline*, or (LWRP).
* **High-Definition Render Pipeline (HDRP)**: The HDRP is designed to produce AAA quality graphics specifically targeted as high-end platforms, making it a good choice for games trying to have cutting-edge graphics.

## Which Renderer Should I use?
The Built-In Renderer, URP, and HDRP are available for 3D games, while 2D only has the Built-In Renderer and URP. 

**In most cases, you will want to go for the Universial Render Pipeline for your projects**. You likely will not have assets to high-fidelity assets to make the cutting edge rendering worth it, and you may find it has a heavier load on your editor.  
Further, the Built-In Render is arguably superceded by the URP. Developers report getting better frame-rates with URP while having easier customization options and better fidelity. 2D URP games also get access to optimized, slick 2D lighting options.

## Switching Renderers
It is technically possible to convert an existing project to a new renderer. However, it can be a massive hassle to do so, as nearly all materials in the project will need to be adjusted in someway, and certain features may become broken.

If you are importing assets from old sources into a URP / HDRP project, you may need to use the *Render Pipeline Converter* to rebuild your shaders and materials if they were made with the Built-In Renderer.