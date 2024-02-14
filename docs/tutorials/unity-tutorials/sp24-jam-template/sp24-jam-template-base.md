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

???+ question "What's in the Box?"
    The starting template comes preconfigured with initialized packages and art assets to make syncing up with the tutorial as painless as possible.

    For your information when you start making your own projects, we've included the following:

    1. A Unity Project using the 2D URP template.
    2. The Unity Input System Package.
    3. Initialized Text Mesh Pro (TMP), with the extra options for additional fonts.
    4. Various Art and UI assets for later modules and experimentation.

    Everything else is up to you to make. Fun!

# Chapter 2: Scene and Art
In this chapter, we will get warmed up with the Unity Editor by building the Game Objects (GOs) for what will eventually be our Player and Enemies. We'll also make quick use of our art assets so we have something pretty to look at.

# Chapter 3: Player Scripts
In this chapter, we'll write some custom behavior scripts which will make our player Game Object move in response to the user's input.

# Chapter 4: Enemy Scripts
In this chapter, we will create (much simpler) script which moves our enemies and kills the player should they touch them.

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