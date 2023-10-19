*Written by Chris DeJong - 4/27/2023*

Creating a window is a crucial step for our application because without a window,
we aren't really doing a whole lot of anything. While the governing code itself is
rather simplistic, the underlying details tend to be a bit complex. As mentioned
in the introduction, we will need to read Microsoft's documentation to really piece
out what to do. I will present these articles to you as we go so that you can follow
the process.

It is also important to not overwhelm yourself with learning the nitty gritty details of Win32
API. The important part is learning the larger concepts of what we're doing; we want to create
a window and define the window procedure. You can always reference the documentation at any point.

## Create a Window

Let's take a moment to familiarize with the process of gathering our required information.
What are we going to do first but to simply Google "win32 create a window"?

[MSDN: Create a Window](https://learn.microsoft.com/en-us/windows/win32/learnwin32/creating-a-window)

This article will most likely be the first link you see and it is precisely what we want.
I highly recommend, before continuing forward, to do this on your own. I promise you that
it isn't hard. Just read through the documentation and do a little copy pasta and you
will probably get a window to launch. If you get stuck, *really* read the documentation or
continue ahead and see the implementation details and explanations.

???+ "Google Searches & You"

    Have you ever heard the expression "Learning how to Google is a skill itself"?
    There is some truth behind that. One of the issues with learning a dense technology
    stack like Win32 and OpenGL is that you need to know how to find the *right* documentation
    amongst all the unimportant ones. You can find a lot of information about any given
    process if you just know how to search for it.

    You will find a good portion of the Win32 API through Google by prefixing a question
    with "Win32" before the question such that you get "win32 create a window tutorial"
    or "win32 how to adjust window size", and the like. You may find yourself on StackOverflow
    in some instances. StackOverflow is a great resource, but I would recommend you use it
    to help you find the proper documentation on MSDN.

    MSDN also includes its own search engine powered by Bing (take that as you will). While
    using this search, you may need to adjust the filter criteria to include "All Documentation"
    in order to find what you're looking for. As you become more familiar with the Win32 API,
    you'll begin memorizing common function names but not the parameter layout. In this
    case, using MSDN's search will be useful to skip straight to the thing you're trying to
    look up.

Hopefully you've managed to create a window on your own. If not, that's okay too. Microsoft
designs their documentation to fit all use cases and provides ample features for those cases
that we aren't necessarily concerned about. It's easy to get lost in the noise, so I will
walk you through the process.

### Window Classes

The first step to creating a window is to create a "Window Class". A window class defines some
of the core properties of window. This registration process is straight forward and it lets the
operating system know what to do when we say "create this window".

[MSDN: Window Class](https://learn.microsoft.com/en-us/windows/win32/api/winuser/ns-winuser-wndclassa)

Take a moment to familiarize yourself with the various struct members using the documentation. Some of them
provide default behaviors for the window, such as the background color, cursor type,
and even how the OS should treat the window when you're doing hardware acceleration.
(This will become important later, but not right now.)

```C++

wWinMain(...)
{

    // Define the window class name. We will need this for the CreateWindow routine as well.
    const char* windowClassName = "wcGameEngine";

    // Create a WNDCLASSA instance and define some essential information.
    WNDCLASSA windowClass = {};
    windowClass.lpfnWndProc   = WindowProcedure;
    windowClass.hInstance     = hInstance;
    windowClass.lpszClassName = windowClassName;

    return 0;
}

```
???+ "IMPORTANT: Regarding "A" and "W" in Win32 Function & Struct Names"

    **This is important, do not skip reading this!**

    Some windows functions that require localization support will postfix their struct
    and function names with "A" or "W". In the above snippet, `WNDCLASSA` is one such
    instance. As you can see, the struct name is postfixed with an "A" and this has
    some important consequences when you write your application.

    The "A" is short for "8-bit ASCII", the typical format of C-strings that you have
    encountered in the past. The above snippet uses "A", and, as a result, the `windowClassName`
    is a normal C-string.

    The alternative to this is "W", which is a 16-bit wide string. The syntax is different.
    If you tried to do the above on your own and encountered strange errors during compilation,
    there is a good chance you weren't using the correct sized string for `lpszClassName`.
    The documentation does use the wide variant:
    
    `const wchar_t CLASS_NAME[]  = L"Sample Window Class";`.

    You will encounter strange bugs if you attempt to interchange "A" and "W" given that
    the compiler doesn't catch it.

    **My recommendation is that you chose either "A" or "W" and stick with it.** I always
    use "A" since it is simpler to deal with and we won't require localization support on
    our application. Any future localization support will be handled contextually within
    the game engine itself, not at the OS level.

We can apply additional parameters to the window class should we so chose, but for now
let's stick with what we have and move on to registering this window class. We can do this
as follows:

```C++

wWinMain(...)
{

    // Define the window class name. We will need this for the CreateWindow routine as well.
    const char* windowClassName = "wcGameEngine";

    // Create a WNDCLASSA instance and define some essential information.
    WNDCLASSA windowClass = {};
    windowClass.lpfnWndProc   = WindowProcedure;
    windowClass.hInstance     = hInstance;
    windowClass.lpszClassName = windowClassName;

    RegisterClassA(&windowClass); // Did you note the "A" here?

    return 0;
}

```

### Creating our Window

Creating our window is as simple as invoking the `CreateWindow` function properly. You
should refer to the documentation and note the parameter requirements yourself, first.

[MSDN: CreateWindowA](https://learn.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-createwindowa)

If you recall previously, the window class name is required during the window creation process.
The name you used in the window class must match the parameter in the create window function.
The operating system will then match the registered window class to the window and apply the
properties we set. Additionally, the create window function will also want the hInstance parameter
from WinMain too, so make sure to supply that.

```C++

// These WinMain parameters are finally useful!
wWinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, PWSTR pCmdLine, int nCmdShow)
{
    ...

	// Execute create window and then handle any errors that may pop up.
	HWND windowHandle = CreateWindowA(windowClassName, "Really Cool Window Title", WS_OVERLAPPEDWINDOW,
		CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, NULL, NULL, hInstance, NULL);

	if (windowHandle == NULL)
	{
		MessageBoxA(NULL, "ERROR: Unable to create window.", "Init Error", MB_OK);
		return -1;
	}
    
    return 0;
}
```

You are free to change the window title to whatever you see fit. Also, take note of the `WS_OVERLAPPEDWINDOW`
styling. Since we are building a GUI application, we want a title bar with a close, min, and max buttons. This
will provide us with all the styling options to achieve that. Additionally, we apply some positioning
and sizing defaults for now. We will come back to this in a future article.

We are *essentially* done with the window creation routine, but there are a few minor details that
need to be taken care of before this compiles and works.

### Window Procedure

We will create a default window procedure in order to make the application run. Unfortunately,
this topic deserves its own article, so we won't go into great detail except to do the minimum.

```C++

LRESULT CALLBACK 
WindowProcedure(HWND hwnd, UINT uMsg, WPARAM wParam, LPARAM lParam)
{
	return DefWindowProc(hwnd, uMsg, wParam, lParam);
}

wWinMain(...)
{
    ...
}

```

Inside the window class, we passed in a pointer to WindowProcedure and now we are defining it.
The window procedure is the method which Windows uses to pass us window and application related
events. Most events are captured here (but not all). The main thing that the current window procedure
is doing for us is the default behaviors, which is more than enough to get the job done.

### Showing the Window

The last step is to show the window.

```C++

// These WinMain parameters are finally useful!
wWinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, PWSTR pCmdLine, int nCmdShow)
{
    ...

	if (windowHandle == NULL)
	{
		MessageBoxA(NULL, "ERROR: Unable to create window.", "Init Error", MB_OK);
		return -1;
	}

    ShowWindow(windowHandle, nCmdShow);
    
    return 0;
}
```

The function itself is explanatory.

## Wrapping Up Window Creation

You should be able to compile and run the application. Since the application itself
is fairly short, I will post the code below in case you have any compilation errors.

```C++
#include <windows.h>

LRESULT CALLBACK 
WindowProcedure(HWND hwnd, UINT uMsg, WPARAM wParam, LPARAM lParam)
{
	return DefWindowProc(hwnd, uMsg, wParam, lParam);
}

int WINAPI
wWinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, PWSTR pCmdLine, int nCmdShow)
{

    // Define the window class name. We will need this for the CreateWindow routine as well.
    const char* windowClassName = "wcGameEngine";

    // Create a WNDCLASSA instance and define some essential information.
    WNDCLASSA windowClass = {};
    windowClass.lpfnWndProc   = WindowProcedure;
    windowClass.hInstance     = hInstance;
    windowClass.lpszClassName = windowClassName;

    RegisterClassA(&windowClass); // Did you note the "A" here?

	// Execute create window and then handle any errors that may pop up.
	HWND windowHandle = CreateWindowA(windowClassName, "Really Cool Window Title", WS_OVERLAPPEDWINDOW,
		CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, NULL, NULL, hInstance, NULL);

	if (windowHandle == NULL)
	{
		MessageBoxA(NULL, "ERROR: Unable to create window.", "Init Error", MB_OK);
		return -1;
	}

    ShowWindow(windowHandle, nCmdShow);

    return 0;
}

```

Once you compiled it, now you can run it.

Don't blink, or you'll miss it!

## Up Next: Window Procedure & Runtime Basics

In the next article, we will learn how to use the window procedure to create a runtime
loop that will let our application continue to run after the window has launched.

Prev: [Platform: Getting Started with Win32](./getting-started-with-win32.md)

Next: Coming Soon!


