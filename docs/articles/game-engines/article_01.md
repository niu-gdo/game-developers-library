# Introduction to Game Engines

Modern game engines are designed to encompass every feature a game designer will need to create their games.
They contain sound engines, lighting logic, animation editors, scripting engines, entity component systems,
custom file I/O libraries, memory management utilities, multithreaded subsystems, and so much more.
When we think of game engines, we often think of game engines like Unreal, Unity, and Game Maker.

The front-end component of these game engines are what we imagine when we think of "game engine".
However, it's important to step away from this line of thinking. You can think of this front-end utility
as "tooling", a subset among the many features that a game engine can offer.

At the simplest level, game engines are graphics renderers with interactive controls. By
building a graphics renderer, you have effectively created a game engine--just add the human interactive
components and you have yourself your own game engine! In fact, the human interactive component
are one of the easier pieces to implement for any game engine.

## Where do we begin?

If you find yourself on Stack Overflow, Quora, or any Q/A website, then you might have
saw an answer along the lines of:

> Why would you create X when Y and/or Z already exist?

I don't like this answer because it stifles creativity and exploration. We all want
to learn how things work and just because it's hard doesn't mean we shouldn't try. Game
engines like Unity and Game Maker exist, but that doesn't mean that learning how to
make a game engine is a fruitless endeavor. I mean, let's be real, we're not going
to compete with triple-A budget studios that made engines like Unreal, but we
really aren't trying to anyway. There is so much we can learn just by *doing*
that long-term success is irrelevant along the way.

But this superimposes the idea that building a game engine
is a venture which you won't complete. I promise you that's not true either.
Knowing is half the battle when it comes to creating a game engine. That's why it
is so hard to even get started, where do we even begin? I mean it, *where do we
even begin?* I will spare you the hypotheticals from this point forward. We will
begin from absolutely nothing. Just you, the computer, and your text editor of choice.

## Knowledge Prerequisites

I will expect that the reader of these articles have some familiarity with C/C++
programming. You should be able to write for-loops, while-loops, functions, and
simple structs with competency. For NIU CSCI students, having completed CSCI 241
would make you well competent in these areas. For those who have not, but feel
rehearsed enough in the above areas, please continue. No better way to learn than
by practice.

You should also be familiar with Windows. Some of you may be Mac users, so having
some basic understanding of Windows will greatly aid you along the way. Being
able to use Window's Terminal (Command Prompt or PowerShell) will be very useful
in the long term.

Lastly, you will need to know how to read API documentation. If you don't, then
you will (need to) learn very quickly. I can not reasonably cover every detail
there is about Win32 and OpenGL, so there will be moments where I will ask you
to reach out to the documentation and piece out what it needs. Trust me, I won't
make you do it for the very important stuff which deserves an explanation.

### System Prerequisites

You will need a computer running Windows 10 or Windows 11. You don't need a gaming
PC or a high end laptop to do anything we are about to do; I imagine that fossils
from mid 2010s could handle what we're about to do, but I would think having a
responsive machine will be a great aid along the way.

Once again, you will need Windows. For our Mac friends out there, the harsh truth
is that both the game industry and Apple are working against you when it comes to
game development. For now, we will only focus on Windows. If you have an Intel-based
Mac, set up a dual boot machine with Windows.

I would highly recommend at least 8GB of RAM, 16GB if you plan to use an IDE or
an IDE-like text editor such as Visual Studio Code.

### Software Prerequisites

You will need a small list of software to get started.

* [Microsoft Visual Studio](https://visualstudio.microsoft.com/downloads/)

    Visual Studio contains the MSVC toolchain which will allow us to compile C/C++
    code to our machine. Once installed, it will launch Visual Studio Installer,
    an update manager / plugin suite where you will select **Desktop Development
    with C++**. This will ensure that MSVC is included with your installation of
    Visual Studio. You can add other packages if you want, but we only need that one.

* [CMake](https://cmake.org/download/)

    We will also want CMake. CMake is a set of tools that makes building binary
    projects easier. We will be using this to help generate our build files. In
    our case, it will be Visual Studio solution files. This isn't a hard and
    fast requirement; you can get away with just Visual Studio itself, but I highly
    recommend that you use CMake instead since it decouples your source files from
    the build tool (which would be MSVC). We won't be interacting much beyond writing
    our initial CMake script and maintaining the list of source files we compile.

    You will need to let CMake add itself to PATH for all users during installation
    to allow it to work via CLI.

* [Git](https://git-scm.com/)

    If you don't already have Git installed, now is the time. You will want to use
    an online source tracking service like Github to manage your project. Whether or
    not it is public or private is up to you. This is a big project, so you want to
    keep your code from disappearing if the rocks in your PC no longer conduct lightning.

* Your Favorite Text Editor

    If you use CMake like I told you, you won't need to use Microsoft Visual Studio
    to write your code. I like Vim, some of you might like VS Code. Whatever environment
    you are comfortable with. Use whatever. (Microsoft Word, anyone?)

## Code Style, Over-Optimization, and Object-Orientated Programming/Design

Before I send you off to write code, let's take a brief moment to talk about the act of
actually writing code. For those that have talked to me in the past, then they might have heard me
express some *opinions* about the current state of software development. Rather than
peppering you with my ideas of how software *should be* throughout each and every
article, I'll get it out of the way so there are no surprises later on.

### The Hot Take: OOP & OOD

I'll come right out of the gate and say that I am not a proponent of Object Orientated
Programming. There are some scenarious which make sense for its use, but its prevalency
throughout the industry and academia is not conducive for effective programming. What
I mean to say is that when we reach into our proverbial toolbox, the first tool we reach
for is OOP and, after awhile, everything starts to look like a nail.

Inheritence and polymorphism introduce significant project complexity when architecting
your application. Such complexity may lead to refactoring down the road as your 
requirements change or new requirements emerge, ultimately reducing the amount of
time producing code that keeps you moving in a forward direction. I rarely use OOP
for this reason. I don't actually know what my application is going to look like at
the end of its development cycle, so I can't make assumptions about the way the API
should be made based on a product that hasn't even been made yet.

Internally, the compiler needs to generate datastructures which manage sub-classed
virtual methods. In instances where performance matters, using inheritence
might be one of the reasons for a dropped frame. There are a lot of areas to
consider when optimizing performance and while virtual lookup tables may not be
the first culprit for performance issues, it is among the few that crop up time
and time again.

I personally don't think that you should change the way you like to program for
the sake of someone's opinions about what the "right way" to program is. I believe
that every developer has a choice to write code the way they like to write it.
However, I would implore you to focus more about writing code that completes the
task at hand rather than writing code you think you will need in the future.

### Over-Optimization and You

This brings us to the next point: over-optimization. We want to write code that is
both fast and easy to write, but rarely do these two things happen together. Throughout
these articles, I will demonstrate code which is the easiest to write. Such code will
probably stay the way it is for a significant amount of time, other times we will
immediately refactor it to account for performance. It's easy to get carried away
with your code and so the first key advice I have for you is to slow down.

One of the best ways to approach any given problem, be it programming or in life,
is to look at with a "first principles" perspective. How would you solve this problem
if you were told to do this using your gut instinct? Your solution need not be elegant,
fast, or thought out. You might be surprised that simple solutions are often some of
the best. Our goal is not to write the best code around, but to write code that gets
us to step two, and then to step three, and so on.

When performance problems arise, they stick out. That's when you optimize.

### Defining Your Code Style

I write code in a very particular way. I liken it more to C than to C++. For object
composition, I use structs to handle my data arrangements. Sometimes, I use static
globals. When I write functions, I write long bodies of code that could be reasonably
decomposed into smaller functions. You could say that I break all the
conventions of what "clean code" looks like.

There are no rules to software development, my friends. If there were, my code
wouldn't compile. My second bit of key advice to you is to find a code style that
works best for you and stick with it. Do not change how you do things mid way through
your project and refactor everything just to meet your new standards. If you absolutely
must, don't refactor, just switch. I don't know of any code base that doesn't look
like a nightmare after line 10,000. That is just what scale looks like.

## Up Next: Setup and Win32 Basics


