*Written by Chris DeJong - 4/19/2023*

Before we can dive right in, there is some paper work to get out of the way. Fortunately,
you will only ever need to do this once since you can easily copy over the structure
to create a new project. It's quite handy if you want to develop in C++ on Windows.

## Preparing the Project Directory & Source Folder Structure

We will begin by creating a folder in `C:\` directory called `Development`. This
will be where we will create our Win32 projects. In the `C:\Development` directory,
create a new directory with a name for your game engine API. Something catchy, preferably.
In this folder, create another folder called `source`. Your project structure should
end up looking similar to this:

```
C:\Development\my-project\
C:\Development\my-project\source
```

???+ note "Other Directories"

    If you want to development somewhere else, that's fine too. We want a location
    that's easy to type an absolute path for, hence why I choose to develop at this
    particular location. This will become apparent down the line when we do some
    file I/O procedures. For now, we won't be using relative paths within our
    program until we examine what happens when we try to do so.

From this point forward, any reference to the *root directory of our project* or some
derivation of this statement will refer to `C:\Development\my-project`. I will also
type out paths such as `./cmakelists.txt` or `./source/main.cpp` to refer to various
files. Take special note here that I will always refer to the root directory in these
instances to be explicity about the file I am referring to. You may want to adopt
your own folder structure, so do your best to keep a mental map of the files as we go along.

You now have the opportunity to initialize Git on your folder and connect it to a Github
repository. Additionally, take the time to get your text editor set up and open. Once
you're ready to pound out some text, create a new file in the root directory of your
project called `cmakelists.txt`.

## Preparing CMake

If you have never used CMake before, you can find a [tutorial here](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)
for your personal reference. There are tons of ways to handle writing a CMake script,
but for these tutorials, I will maintain a single CMake script in the root directory
for the sake of simplicity.

The below script is one that I use for all my projects. All I do is add source files
within `add_executable(...)` as I make them. Be sure to change the name of `project()`
to a name of your choice. This name will reflect the name of the executable, but
you can change that under `add_executable` by replacing `${PROJECT_NAME}` to a string
of your choice.

```
# Initialize the CMake version
cmake_minimum_required(VERSION 3.21)

# Set the project name. Change this to the appropriate name as desired.
project(my-project)

set(CMAKE_C_STANDARD 11)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

add_executable(${PROJECT_NAME} WIN32

"./source/main.cpp"

)

# Search for OpenGL if we need it.
find_package(OpenGL REQUIRED)

# Set Visual Studio's startup project to the base project.
if (MSVC)
	set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME})
endif ()

# Allow absolute referencing for project files located in ./src
target_include_directories(${PROJECT_NAME} PUBLIC ./source)

# Include OpenGL libraries.
target_link_libraries(${PROJECT_NAME} opengl32.lib winmm.lib)

```

This CMake script also sets up a couple extra things we will need along the way.

1. We ensure that we have OpenGL and any Win32 libraries linked to our executable
at compile time. Since we are not given these libraries by default, we need to link
them ourselves.

2. We also configure CMake to let us use angle bracket notation to access our header files.
Rather than typing `#include "main.h"` or `#include "../../core/my_header.h"`,
we can simply use `#include <main.h>` and `#include <core/my_header.h>` respectively. Neat.

3. For sanity purposes, we force Visual Studio to generate a solution file with our
project file as our default project when it loads. If you don't, it will get annoying fast.

## Preparing an Entry Point

The last step in our setup is getting something to compile. Go ahead and create a
file called `./source/main.cpp` and write a simple "Hello, World" program.

```C++
#include <iostream>

int
main(int argc, char** argv)
{
    std::cout << "Hello, world\n";
    return 0;
}
```

From here, you will need to "configure" your CMake project by running this command
at the root directory of your project:

```
cmake . -B./build
```

This command will
create a folder called `./build` which contains everything MSVC needs to compile
your project. You only need to run this command once to generate your project files.
You may need to run this again if you change your CMakeLists file or delete the `./build`
folder. If you encounter any weird errors while building (except for the one we are
immediately about to see), 9 times out of 10, deleting the `./build` folder and
reconfiguring your project will fix it. Additionally, you may want to create a `./.gitignore`
file which excludes this directory since it can be generated on the fly fairly quickly.

Now, to compile your program, you will once again use CMake by typing the command at
the root directory of your project:

```
cmake --build ./build
```

This command will invoke MSVC on your project files. You
will need to use this command every time to compile your project or go into your
`./build` folder and open the Visual Studio solution file and compile through Visual
Studio.

If you did everything correctly, you probably got an error fairly close to this:

```
error LNK2019: unresolved external symbol WinMain referenced in function
"int __cdecl invoke_main(void)"
```

## Up Next: Getting Started with Win32

In the next article, we will look at programming for Windows. We will look at the
above error, how to correct it, and why it exists in the first place.

Prev: [Introduction to Game Engines](./introduction-to-game-engines.md)

Next: [Platform: Getting Started with Win32](./platform/getting-started-with-win32.md)
