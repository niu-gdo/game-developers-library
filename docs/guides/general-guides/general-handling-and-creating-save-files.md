# Handling and Creating Save Files

*By Jake Rogers*

## Introduction

Video games often need to create persistant data files in order to store information. For instance, storing the player's preferred settings and reloading them from a file each time the game starts would be great instead of having them change their settings every reload- in fact, this is **expected** behavior.

We may also want to store record information, such as the user's top score on a leaderboard, levels / cosmetics they have unlocked, and other things related to game progression and scoring.

Most importantly, larger games will sport some kind of system for saving and reloading entire game states from a file, allowing the player to continue where they left off after shutting down the game or even just reloading the game while playing to undo a mistake.

In this guide, we will discuss the design parameters regarding these save systems and detail some common approaches and use cases.



## Creating Files

In order to create some persistent store for data, we will use a strategy you may be familiar of from other programming approaches: creating a file somewhere on the user's storage devices and filling it with data in a format which we can later parse to get our information back at.

The first obvious question is *where* should we save our files to? It needs to be some location on the user's file system that is guaranteed to exist **and** has write permissions. You may also need to consider multi-platform support, as a Windows file structure will not be the same as a MacOS or Linux one.

Fortunately, if you are using a game engine, this question is almost certainly handled for you. They typically give you some kind of *persistent data path*, which is a route to a folder on the user's system which is **guaranteed** to be writable for our purposes. Not only does this typically work for desktop machines, but it is also usually a valid path for mobile devices as well.

For example, Unity's Windows data path is a file in the `AppData` substructure organized under your organization name, then the game's name. You can then write as many files as you would like under this directory (at least until the user's OS stops you).

* [Unity's Data Paths](https://docs.unity3d.com/ScriptReference/Application-persistentDataPath.html)
* [Unreal uses a SaveGame Class Which Routes For You](https://docs.unrealengine.com/4.26/en-US/InteractiveExperiences/SaveGame/)
* [Godot Data Paths](https://docs.godotengine.org/en/stable/tutorials/io/data_paths.html)

If you do not use an engine which provides this feature to you, it is likely a good idea to try and use the above data paths as an example. You will have to handle your own multi-platform support if needed.

## Storing Data in Files
Once we have a reliable file we can write to, we must then decide what needs to be saved and **what format would be best for saving it**.

Note that the actual implementation of saving data will vary largely based on the engine or language being used. Some may have built in libraries for generating entire JSON files from your input data, others may require explicit file writing procedure.

### Data Sensitivity
The format we chose for saving our data will largely depend on how **sensitive** the data is. Since players will be saving these files to their machines, it is possible that savvy users may try to read or edit these files themselves in order to view alter the data saved in the file.

Depending on the contents of the file, we may wish to prevent them from doing this or assist them in doing this.

#### Sensitive Data
Sensitive data should often not be seen, and definitely not be altered by users. Things related to your game's state such as character positions, player health, ammo count, current level, achievements, etc. should be considered sensitive data, since changing them could be considered cheating **or could corrupt the user's game if incorrect values are entered**

Sensitive data is almost always stored in a binary format, meaning that the values we need to save are stored back-to-back in bytes. These resultant binary files are not human readable, but are often significantly smaller than insensitive storage methods like text or JSON since whitespace is omitted and data is typically smaller in byte-format than in ASCII.

However, binary save data requires some keen engineering to properly implement compared to a key-value style format like JSON. Let's say that our game requires us to save a character's health and armor (floating point), level (integer) and position (An X,Y,Z floating point value).

The health and armor,

#### Insensitive Data
A good example of insensitive data would be something like configuration settings: The screen resolution, volume settings, keybindings, graphics preferences, etc. Something like a log / output file would also fall under this category.

One could argue that it is actually okay to allow users to modify these files, since it may give them a greater degree of control than our user interfaces can allow. Further, users may wish to share configuration files with each other.

Since log files generally do not need to be read, they can simply be written in a textual format, easy!

However, 