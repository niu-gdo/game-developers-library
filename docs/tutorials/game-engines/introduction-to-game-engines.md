---
title: Introduction To Game Engines
summary: At the simplest level, game engines are graphics renderers with interactive controls.
description: At the simplest level, game engines are graphics renderers with interactive controls.
authors:
    - Chris DeJong
date: 2023-04-19
---
*Written by Chris DeJong - 4/19/2023*

Modern game engines are designed to encompass every feature a game designer will need to create their games.
They contain sound engines, lighting logic, animation editors, scripting engines, entity component systems,
custom file I/O libraries, memory management utilities, multithreaded subsystems, and so much more.
When we think of game engines, we often think of game engines like Unreal, Unity, and Game Maker.

The editor of these game engines are what we imagine when we think of "game engine".
However, it's important to step away from this line of thinking. You can think of this editor
as "tooling", a subset among the many features that a game engine has to offer.

At the simplest level, game engines are graphics renderers with interactive controls. By
building a graphics renderer, you have effectively created a game engine--just add the human interactive
components and you have yourself your own game engine! In fact, the human interactive component
are one of the easier pieces to implement for any game engine.

## Where do we begin?

Suppose you ask yourself this simple question:

> How do I create a game engine?

If you find yourself on Stack Overflow, Quora, or any Q/A website, then you might have
saw an answer along the lines of:

> That would be too difficult. Why would you want to do that when "X" and "Y" already exist?

This response is what stifles creativity and hinders exploration. We all want
to learn how things work and just because it's hard doesn't mean we shouldn't try. It is true that game
engines like Unity and Game Maker already exist, but that doesn't mean that learning how to
make a game engine is a fruitless endeavor. I mean, let's be real, we're not going
to compete with triple-A budget studios that created games engines like Unreal, but
there is so much we can learn just by *doing* that long-term success is irrelevant.

But this superimposes the idea that building a game engine is a venture that you won't complete.
I promise you that's not true either. Knowing is half the battle. That's why it's so
difficult to get started. Once you know what you're looking for, it's very easy to
pave your own path and explore.

By the end of these articles, you will have sufficiently learned enough about game
engines to create a game from scratch. You will be surprised that there really isn't
much to it. How far you want to go is what will end up determining how much work
you will need to put in.

## Prerequisites

### Knowledge Prerequisites

I will expect that the reader of these articles to have some familiarity with C/C++
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
    the build tool (which would be Visual Studio/MSVC). We won't be interacting with CMake scripting
    much beyond writing our initial CMake script and maintaining the list of source files we compile
    within said script.

    **Note:** You will need to let CMake add itself to PATH for all users during installation
    to allow it to work via CLI since we will be using the CLI to configure and build
    our CMake scripts.

* [Git](https://git-scm.com/)

    If you don't already have Git installed, now is the time. You will want to use
    an online source tracking service like Github to manage your project. Whether or
    not it is public or private is up to you. This is a big project, so you want to
    keep your code from disappearing if the rocks in your PC no longer conduct lightning.

* Your Favorite Text Editor

    If you use CMake, you won't need to use Microsoft Visual Studio to write your code.
    I personally use Vim, others prefer VS Code. Use whatever editor you are the most
    comfortable with. (Microsoft Word, anyone?)


???+ note "System Prerequisites"

    You will need a computer running Windows 10 or Windows 11. You don't need a gaming
    PC or a high end laptop to do anything that we are about to do. I imagine even
    a ressurected fossil will be able to reliably run our application with minimal
    effort. However, to have full access to the suite of development tools that Microsoft
    provides us, having an up-to-date operating system is key to long-term success.

## Code Style, Over-Optimization, and Object-Orientated Programming/Design

Before I send you off to write code, let's take a brief moment to talk about the act of
actually writing code. Throughout these articles, you will find that I am not using
object-orientated programming for many of the problems that we are encountering. You
are free to approach these problems with OOP if you so desire.

### Over-Optimization and You

Let's talk about something fairly important: over-optimization. We want to write code that is
both fast and easy to write, but rarely do these two things happen together. Throughout
these articles, I will demonstrate code which is the easiest to write. Such code will
probably stay the way it is for a significant amount of time, other times we will
immediately refactor it to account for performance. It's easy to get carried away
with your code and so the first key advice I have for you is to slow down.

One of the best ways to approach any given problem, be it programming or in life,
is to look at the problem with a "first principles" perspective. How would you solve this problem
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

## Up Next: Win32 Environment Setup

In the next article we will set up our development environment using CMake and
get everything we need to start developing our game engine.

Next: [Win32 Environment Setup](./win32-environment-setup.md)
