*Written by Chris DeJong - 4/20/2023*

If you haven't followed the [previous article yet, please do so now](../win32-environment-setup.md)
as it will get you caught up to speed on where we last left off. As a short recap, we setup
our Win32 environment by creating a traditional "Hello, World" program, but encountered a
strange error when compiling.

## The Entry Point

At some point during Microsoft's transition from MSDOS operating system
to the current era of Windows we know it today, they made some decisions about how application
types are handled at the kernel level. These early decisions meant that there is
split between "Console Sub-System" applications and "Windows Sub-System" applications.
When we create "Windows Sub-System" applications, Windows automatically provides us
key libraries to interact with the kernel, but in turn strips us of the console under
the expectation that we won't be needing it.

???+ "Could we re-hook a console?"

    You absolutely can, but not in the way you think. You see, Windows doesn't make
    this easy for us, so it is much easier to allocate a new console for us to perform
    standard input and output to. We will not be doing that for these articles because
    it won't be useful for what we're trying to do. In the rare instances we actually need a console,
    MSVC contains compiler intrinsics for us to use that integrate with Visual
    Studio which act as an interface for console output.

    I also don't want you to use the console as a crutch for debugging. Programming
    a game engine will get complex, so learning how to use Visual Studio to debug
    your program will be necessary down the line and, by forcing you to use it right
    out of the gate, it will teach you how to use it.

### Transition from Main to WinMain

In order to get our program to compile, we will need to define a new entry point
called WinMain. You can think of WinMain as a "higher order" entry point with
additional parameters that Windows provides us for interacting with the Win32 API.
These parameters aren't going to be entirely important in the long run, but you
can find information here:

[MSDN: WinMain, Application Entry Point](https://learn.microsoft.com/en-us/windows/win32/learnwin32/winmain--the-application-entry-point)

[MSDN: WinMain Documentation](https://learn.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-winmain)

For now, let's just replace everything within `./source/main.cpp` with this:

```C++
#include <windows.h>

int WINAPI
wWinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, PWSTR pCmdLine, int nCmdShow)
{
    return 0;
}

```

### Compiling with WinMain

At this point, you should be able to correctly compile your program. As you might
imagine, the program won't actually do anything, but let's run it anyway and see
what happens. You will need to navigate to your `./build/bin/Debug/my-project.exe`.
The name of the executable reflects what you set in the `./cmakelists.txt` file.

Nothing will happen.

Let's go back to `./source/main.cpp` and add a line within main:

```C++
...
wWinMain(...)
{
    MessageBoxA(NULL, "Hello, world\n", "My Cool Message Box", MB_OK);
    return 0;
}
```

???+ "Regarding Code Snippets"

    I will be dropping code snippets with elipses `...`. This is not code, rather it is to
    indicate where code *is*. When we write large bodies of code, or add code to
    large bodies of code, I want to make it easy for you to find where exactly it is
    that I am adding the code, so I will copy a recognizable chunk and then omit
    portions to reduce the size of the snippet.

    In the above example, I leave an elipsis above `wWinMain` and between the brackets
    as `wWinMain(...)` to indicate that there is code there, but it isn't important
    for the code snippet.

    I will do my best to make it obvious where I am working and provide comments
    for the code that I am adding if it isn't clear in the snippet.

When you compile this and attempt to run the application, you should get a pop up.
Hit ok, the application will close.

**Congratulations! You have written your first Win32 program!**


## Up Next: Creating a Window

In the next article, we will look at how to create a window with the Win32 API
and message procedures necessary to operate with windows.

Prev: [Win32 Environment Setup](../win32-environment-setup.md)

Next: [Creating a Window](./creating-a-window.md)
