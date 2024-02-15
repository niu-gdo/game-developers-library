# Spring 2024 Game Jam Template - Base Tutorial
*By Marceline Gallegos and Jake Rogers*

*Created: February 7th, 2024*

# Summary

Since the GDL already has articles on the basics of Unity use, we will not repeat ourselves here. Please view the articles below if you are stuck with the following topics:

* Installing Unity (Read: [Tutorial Here!](/tutorials/unity-tutorials/first-step-series/unity-first-step-install))
* Basic Editor Controls (Read: [Tutorial Here!](/tutorials/unity-tutorials/unity-editor-introduction))

# Chapter 1: Project Set-Up
Visit [this project's GitHub Page](https://github.com/niu-gdo/game-jam-template-sp24) and follow the instructions to download the starting template. 

**Be sure to select the 'base-template' branch before cloning or downloading the ZIP.**

??? question "What's in the Box?"
    The starting template comes preconfigured with initialized packages and art assets to make syncing up with the tutorial as painless as possible.

    For your information when you start making your own projects, we've included the following:

    1. A Unity Project using the 2D URP template.
    2. The Unity Input System Package.
    3. Initialized Text Mesh Pro (TMP), with the extra options for additional fonts.
    4. Various Art and UI assets for later modules and experimentation.

    Everything else is up to you to make. Fun!

Once you have the project open in Unity, take a brief second to **regenerate your project files for Visual Studio**. This is done by selecting along the top `Edit -> Preferences... -> External Tools -> External Script Editor -> Visual Studio 2022 / 2019`. 

Then, press the '*Regenerate project files*' button.

![](./base-res/regenerate-project-files.gif)

??? question "Why Did I Need to do That?"
    Some files that Visual Studio uses to provide many contextual coding features are often not uploaded to source control systems, so they won't be included when you clone or download from a repository.

    Therefore, it is usually a good idea (unless told otherwise) to regenerate these project files when you first download a repository before you wonder why everything looks broken in Visual Studio!

Lastly, whenever you download a new Unity project, Unity typically doesn't know what scene it should open, so you'll wind up on an empty, unsaved one. Before continuing, open the `Scenes` folder in the *Project* window and open the *SampleScene*.

# Chapter 2: Scene and Art
In this chapter, we will get warmed up with the Unity Editor by building the Game Objects (GOs) for what will eventually be our Player and Enemies. We'll also make quick use of our art assets so we have something pretty to look at.

### Adding the Background
The default grey background is pretty ugly, so let's pull in our background art to quickly remedy that.

In the project window, find `Art -> Backgrounds -> darkPurple`. This is a tilable PNG background which we can use to cover the entire screen space. Drag the *darkPurple* image asset into an empty space on the *Hierarchy* window to add it to the scene (ensure it hasn't been made a child of anything else).

If you were to try and resize the sprite using the *Scale* or *Rect* tool, you'll notice that it just stretches and distorts, which looks terrible. Instead, we must *tile* the sprite to allow it to repeat across a region instead of stretching.

To do so, select the new sprite we added to the *Hierarchy* to view it in the *Inspector*. Make the following changes:

* Draw Mode: Tiled
    * Size, Width: 35
    * Size, Height: 35

This will accomplish the desired tiling effect, which looks much better than stretching it! Let's also rename the Game Object from '*darkPurple*' to '*Background*'.

Lastly, you may have noticed that the background's Inspector window is displaying a warning about the sprite's Mesh Type. We'll resolve this by doing exactly what it says: Select the `Art -> Backgrounds -> darkPurple` asset in the *Project* window and change the Mesh Type to 'Tiled', then hit apply.

![](./base-res/add-tilable-background.gif)

Note that you can of course use any of the other backgrounds provided if you like them more, and you can also select the sprite Game Object and change it's *Color* property to tint them as well!

### Creating the Player Game Object

# Chapter 3: Enemy Scripts
In this chapter, we will create (much simpler) script which moves our enemies and kills the player should they touch them.

# Chapter 4: Player Scripts
In this chapter, we'll write some custom behavior scripts which will make our player Game Object move in response to the user's input.


# Chapter 5: Laser Gun
In this chapter, we'll create the feature which allows the player to fire lasers that can destroy enemies.

# Chapter 6: Spawner
Almost done! In this final chapter, we'll create a spawner which will periodically shoot some enemies into the scene!

# Conclusion
Congratulations, you've now got a pretty neat game and some basic concepts under your belt! 

### What now?

This game, as is mentioned in the article's title, works as a great *template*- you can learn a lot by expanding it with your own features and experimenting. There is a lot you can do to make your version of the game unique from everyone else's, you may have already had some ideas, so try and implement them!

Keep in mind as well that you can completely charge around the art assets if you're not digging the space theme- the top down controller could be used in something like a hunter dodging leopards in the jungle, ships at sea, or a dungeon crawl. Be creative!


#### Ideas for Expansion
Here are some ideas of things you could do if you need inspiration:

* Add sound effects and particle effects for player / enemy death, laser shooting, flying, etc. This will really make your game pop!
* Create a game over screen when the player dies which reports time survived, allows them to restart and quit the game.
* Create a main menu before the game starts.
* Fix the bug which allows the player to fly off the screen boundaries.
* Make the enemies spawn faster as the player survives longer.
* Create some new enemy types:
    * A slower but much larger enemy.
    * An enemy which breaks into two smaller ones when destroyed.
    * An enemy which takes multiple shots to destroy.
* The player has a health bar that constantly drains- it can only be restored by picking up health dropped by destroyed enemies.
* Add some more detail to the background- far off planets, asteroids flying around, etc.

In the future, this tutorial will be expanded with additional modules to show you how to do some of these things. Look forward to that!