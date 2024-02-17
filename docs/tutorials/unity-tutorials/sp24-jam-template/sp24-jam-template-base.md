# Spring 2024 Game Jam Template - Base Tutorial
*By Marceline Gallegos and Jake Rogers*

*Created: February 7th, 2024*

# Summary

Since the GDL already has articles on the basics of Unity use, we will not repeat ourselves here. Please view the articles below if you are stuck with the following topics:

* Installing Unity (Read: [Tutorial Here!](/tutorials/unity-tutorials/first-step-series/unity-first-step-install))
* Basic Editor Controls (Read: [Tutorial Here!](/tutorials/unity-tutorials/unity-editor-introduction))

Please also note, most images and gifs on this page can be viewed in full size by Right-Clicking them and selecting 'Open Image in New Tab'. Please do so if they are hard to read.

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

### Creating the Enemy and Player Game Objects
Let's take a moment to discuss exactly what our player and enemies will do. 

Our enemies are simple, they will...

* Float across the playable area in a single direction.
* Upon colliding with the Player, destroy both the Player and themselves.

Our Player will be slightly more complicated:

* Fly around in any direction using the WASD keys, coming to a stop with no input.
* Rotate towards the direction it is flying in.
* Shoot lasers which can destroy enemies.

While we're on the topic of pulling in our art, let's set up the visuals and initial Game Objects for the enemies and Player right now.

##### Player
Start by Right-Clicking on the *Hierarchy* window and selecting 'Create Empty'. Name the new Game Object *'Player'*. 

We'll then add a empty Game Object to the *Player*. Do this by right-clicking *Player* and 'Create Empty' on that. Name the new child object *'Visuals'*

Lastly, we'll add a sprite the *Visuals* object which will be our graphics for the Player. Right-Click on *Visuals* and do `2D Object -> Sprite -> Square`. Name it *Base Sprite*. 

On *Base Sprite*, we can use whatever sprite we would like for our player by dragging it into the `Sprite` field. You can find a bunch of very suitable candidates in `Art -> Sprites` within the *Project* window. I'll be using *playerShip2_red*.

??? tip "Selecting Reference Types"
    In addition to supporting drag-and-drop, reference-type fields will often allow you to press the circular-selector button to see all items in the project that can fill in the field, which you can then search from. 
    
    This is often a much faster way to fill in things from the inspector if you don't have them already visible in the *Project* window!

You __may__ have noticed an issue here, which is that the Player sprite appears to be drawing *underneath* the background, thusly making it not visible (This may or may not occur depending on a couple of factors, but it needs to be fixed regardless).

To fix this, we need to set up *Sprite Sorting Layers* which define what groups of sprites should render on top of others. Fold out the *Layers* drop down button in the top-right of the editor, and select '*Edit Layers*'.

You can then fold down the *Sorting Layers* list and press the `+` button to add a few more. I'll be using the following layers **in this specific order**:

* 0) Background
* 1) Default
* 2) Projectile
* 3) Enemy
* 4) Player

Things at the bottom of the list will *always* render in front of things closer to the top of the list.

Select the *Background* and change the *Sprite Renderer*'s `Sorting Layer` to `Background`. Change the Player's *Base Sprite*'s `Sorting Layer` to `Player`. There should be no rendering conflicts now!

##### Enemy
We've got a great opportunity to be lazy here. Let's duplicate the *Player* Game Object (select it and press ++ctrl+d++), then rename it to *'Enemy'*. You can then change its *Base Sprite*'s `Sprite` to one of the asteroid sprites. I'll be using `Art -> Sprites -> meteorBrown_big1`.

Don't forget to change sorting layer for the enemy's base sprite to `Enemy` instead of `Player`, and you're done!

# Chapter 3: Enemy Scripts
In order to get our enemies to do exactly what we want them to, we'll need to write custom scripts to dictate how what they should do when the game runs through code. Since the design goals for the Enemy are much simpler than for the Player, we'll start on the Enemy.

### Component Set Up
Before we write our own script, we'll need to do a little more configuration on the *Enemy* Game Object before hand.

To start, whenever we want to allow a Game Object to move in anything besides the most simple of ways, we generally want to add a *Rigidbody* (Or *Rigidbody2D* if you're using 2D, which we are!) component. Doing so allows the Game Object to do the following:

* Move at run time using the Unity Physics System and be affected by various kinematic forces.
* Register collisions with other Rigidbodies.

We would like to do both of those, so select the *Enemy* Game Object and do `Add Component -> Rigidbody2D`.

If you enter play mode immediately after doing so, you'll actually notice your enemy fall off the screen due to the implicit gravity force that Rigidbody2D's come initialized with!

We don't really want gravity here though. In fact, we would like to have very explicit control over how our enemy moves (In other words, we don't want the physics engine doing anything to it unless we code it that way). Fortunately, changing the Rigidbody2D's `Body Type` property to `Kinematic` in the *Inspector* will do exactly that- the Enemy will no longer be affected by gravity or bounced around by other objects. Cool.

Before we continue, we do still need to add a *Collider* to this Game Object configured to be a Trigger so that we can tell when it hits the Player. Do `Add Component -> Circle Collider` to do so. Check the `Is Trigger` property, and press the `Edit Collider` button to change the hitbox to your liking (or use the `Radius` property to numerically change the size).

Great! That's all the set up we need to start scripting!

### EnemyController Script
Let's now build the script that will add our custom behavior for these Enemies. In the Scripts folder within the *Project* window, Right-Click and do `Create -> C# Script`, name it *'EnemyController'* and double-click to open it in your code editor.

Once we are done writing this script, we will be able to place it onto our *Enemy* Game Object as a component (just like the Rigidbody2D and Sprite Renderer) to apply the custom behavior.

##### Movement

For now, we'll write the following code in `EnemyController.cs`:

```cs title="EnemyController.cs" linenums="1"
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class EnemyController : MonoBehaviour
{
    private Rigidbody2D _rigidbody;     // The rigidbody component on this enemy

    // Start is called before the first frame update
    void Start()
    {
        _rigidbody = GetComponent<Rigidbody2D>();

        _rigidbody.velocity = new Vector2(0f, 5f);
    }
}
```

???+ abstract
    Every script which derives from the `MonoBehavior` class will have a series of Events called on it at various times by Unity's script runner or other activites in your game. `void Start()` is one such Event- and the code within it starts once the Game Object the script is attached to enters the scene for the first time. This makes it a good place for initialization.

    To get our *Enemy* to move, we need to set the velocity on its *Rigidbody2D* component we attached through code- it'll fly in whatever direction we specify.

    Therefore, when the game starts, we use `GetComponent<Rigidbody2D>()` (Line 7) to search for the Rigidbody and store a reference to it- then set it's velocity to an upwards-pointing vector (0 on the X axis, 5 on the Y).

Return back to Unity and attach the new `EnemyController` component to the *Enemy* Game Object, then enter play mode to watch it fly off the top of the screen!

##### Movement Adjustments
There two things we would like to change about how we move the Enemy. First- in order to change the Enemy's speed, we currently have to go back into the code, change it, and recompile it. Not only is this a hassle, but it also means *all* enemies have to move at the same speed, which is very inflexible.

To fix this, make the following adjustments to the code:
```cs title="EnemyController.cs" linenums="1" hl_lines="7 8 17"
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class EnemyController : MonoBehaviour
{
    [SerializeField, Tooltip("The enemy's movement speed in units per second")]
    private float _movementSpeed = 2f;

    private Rigidbody2D _rigidbody;     // The rigidbody component on this enemy

    // Start is called before the first frame update
    void Start()
    {
        _rigidbody = GetComponent<Rigidbody2D>();

        _rigidbody.velocity = new Vector2(0f, _movementSpeed);
    }
}
```

???+ abstract
    Adding the new class member `_movementSpeed` and putting the `SerializeField` tag before it allows this value to be set in the *Inspector* window- so we can adjust it in the editor (even while the game is playing)!

    We then use that `_movementSpeed` in place of the hard-coded `5f` speed.

If you go back to the editor and look at the *Inspector* for *Enemy*, you will see a new `Movement Speed` field which you can type custom values into. As mentioned in the Abstract, you can even adjust this value while in play mode!

---

The second issue we'd like to fix is that currently, the enemies will **only** ever move in the up direction (positive on the Y axis, assuming `Movement Speed` is positive). As you may have noticed in the thumbnail, we have enemies moving in any kind of direction, so let's fix that!

For this game, we use any projectile's Y-Axis (The *green* one, colloqually the *Up Axis* in 2D) as it's forward direction. Therefore, our Enemy's velocity should travel in that direction.

??? question "How Can I Tell What Direction a Game Object is 'Facing'?"
    In the Editor, select a Game Object, then ensure your rotation mode (Located in the top left of the *Scene* window, next to the tool shelf) is set to `Local`, not `Global`. 
    
    You can then look at the direction of the *Green* arrow to see the orientation of the object.

    You can rotate the Game Object to observe this Up-arrow change direction.

This is a lot simpler to do than it probably sounds, and just involves changing one line:
To fix this, make the following adjustments to the code:
```cs title="EnemyController.cs" linenums="1" hl_lines="17"
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class EnemyController : MonoBehaviour
{
    [SerializeField, Tooltip("The enemy's movement speed in units per second")]
    private float _movementSpeed = 2f;

    private Rigidbody2D _rigidbody;     // The rigidbody component on this enemy

    // Start is called before the first frame update
    void Start()
    {
        _rigidbody = GetComponent<Rigidbody2D>();

        _rigidbody.velocity = transform.up * _movementSpeed; // Set the linear velocity of this enemy in units per second.
    }
}
```

???+ abstract
    `transform.up` provides a directional Vector which matches the Green arrow of the Game Object the script is attached to. We can then multiply that Unit Vector by our `_movementSpeed` to make it move according to our desired speed.

    For example, now if our enemy is pointed towards the right, the velocity will be set to `(1, 0) * 2`, rather than `(0, 1) * 2`. Similarly, if it's pointed diagonally down and to the left, it will be `(-0.66, -0.66) * 2`.

    Note that you can get the direction for any of the local axes via `transform.right` and `transform.forward` (3D). You can also *set them* to a particular value to align the Game Object's axis with the direction you provide, which is *VERY USEFUL*.

As a side note, don't be put off if the talk of Vectors and Directions is a little lost on you- it can take a moment for it to click into place for some. If it doesn't come naturally, feel free to look up some supportive information- this article from Unity is a good start:

[Unity's Vector Cookbook](https://docs.unity3d.com/560/Documentation/Manual/UnderstandingVectorArithmetic.html)

(Note that these pages report as legacy, but all information is valid since it's mathematics. Be sure to use the `->` buttons to view additional pages)

Anyways, rotate your Game Object to change it's up direction and play it will now travel in the correct direction!

### Destroying the Player
We will modify our `EnemyController` script to do the following:

1. Watch out for any objects entering the enemy's trigger collider.
2. Upon a trigger collision, check to see if the thing we collided with is the *Player*.
3. If so, destroy both of us.

Let's implement that with the following code on `EnemyController`:
```cs title="EnemyController.cs" linenums="1" hl_lines="20-23"
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class EnemyController : MonoBehaviour
{
    [SerializeField, Tooltip("The enemy's movement speed in units per second")]
    private float _movementSpeed = 2f;

    private Rigidbody2D _rigidbody;     // The rigidbody component on this enemy

    // Start is called before the first frame update
    void Start()
    {
        _rigidbody = GetComponent<Rigidbody2D>();

        _rigidbody.velocity = transform.up * _movementSpeed; // Set the linear velocity of this enemy in units per second.
    }

    private void OnTriggerEnter2D(Collider2D collision)
    {
        Destroy(collision.gameObject);
        Destroy(gameObject);
    }
}
```

???+ abstract
    `void OnTriggerEnter2D(Collider2D)` is another Unity Event- this one will run whenever another collider enters the Trigger Collider present on this Game Object (with the `collision` parameter being the other collider detected).

    Quite simply, we will use the `Destroy(GameObject)` method to destroy the other thing we collided with, then Destroy ourselves.

Note, however, that the code above will cause the enemy to destroy *any* thing is collides with, not just the Player.

There are a couple ways to determine if the thing we collided with is a particular Game Object we're looking for, but the most common way is to check to see if it has a particular component unique to Player.

In Chapter 4, we'll need to add a `PlayerController` to our Player, so let's go ahead and do that now so that we can search for that component while doing collsion resoluton.

In the Project Window, make a new `PlayerController` C# Script, add it as a component to the Player (we do not need to edit the script yet), then make the following changes to `EnemyController`:
```cs title="EnemyController.cs (fragment)" linenums="20" hl_lines="20-23"
private void OnTriggerEnter2D(Collider2D collision)
{
    // On collision with another game object, check if it's the player.
    // If so, destory it and this enemy.
    if (collision.GetComponent<PlayerController>() != null)
    {
        Destroy(collision.gameObject);
        Destroy(gameObject);
    }
}
```
???+ abstract
    Upon hitting another collider, we'll search its Game Object to see if it has a `PlayerController` component. Since `GetComponent` will return `null` if it cannot find the type searched for, we can check against that.

    If a `PlayerController` is found, then we can procede with destroying the Player and the Enemy.
    
    If you'd like, you can confirm this works by ++ctrl+d++ duplicating the *Enemy*, rotating them to collide with one another, and witnessing them pass through one another harmlessly!

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



# Appendix

#### Why Do We Organize Our Player and Enemy Game Objects so Elaborately?
    
#### Why Do We Use Triggers Colliders Instead of Regular Colliders?