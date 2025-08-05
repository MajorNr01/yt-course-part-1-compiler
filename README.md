# Introduction

The goal of this tutorial is to get you set up for building C++ software for both Windows and Linux operating systems. I try to focus on the commonalities between the build processes on each OS. The project file, source code and build commands are the same in both cases.

# Required Tools

* Git
* GCC
* Make
* CMake
* Your text editor of choice

# Windows 11 (MSYS 2)

Install MSYS 2 from https://www.msys2.org/. The installation may take several minutes.

Now, open MSYS 2 in the MINGW64 Environment. On Windows 11, press the `WIN` key and type `MSYS2 MINGW64`. You can read more about MSYS 2 environments at https://www.msys2.org/docs/environments/ if you're interested.

Install packages:

* git
* mingw-w64-x86_64-gcc
* make
* cmake

````
pacman -S git mingw-w64-x86_64-gcc make cmake
````

# Ubuntu 24.04.2 LTS (WSL)

Set up Windows-Subsystem for Linux (WSL) by running:

````
wsl --install
````

in PowerShell or Command Prompt. You'll likely have to choose a distro and set up a user. This tutorial assumes that you chose Ubuntu.

> **NOTE:** I use WSL to run an Ubuntu VM because it is convenient for me right now. The following steps will work on any Ubuntu Linux machine.

Install packages:

* git
* build-essential (gcc, make)
* cmake

````
sudo apt-get update && sudo apt-get install -y git build-essential cmake
````

# Files

You'll need at least the following files: `CMakeLists.txt` and `main.cpp`: A project configuration file and a source code file.

## CMakeLists.txt

````
cmake_minimum_required(VERSION 3.22)

project(FIRST_STEPS)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS "-static")

add_executable(first-steps
    main.cpp
)
````

This is your project file. Here you configure the compiler and list your source files, including headers. The first two lines are basically boilerplate. You choose which version of CMake you want and the name of your project within your CMake configuration.

Then we require C++ version 17 and add the `-static` flag to avoid as many external dependencies as possible.

> **NOTE:** The `-static` flag is a GCC linker option and will not work with other compilers.

Finally, we define an executable from a list of files, in this case only our `main.cpp` file.

I remember having trouble getting into reading and writing CMake. It's a strange language but you should learn it if you want to build C++ software. You can learn more about it here: https://cmake.org/cmake/help/latest/manual/cmake-language.7.html

## main.cpp

````
#include <iostream>

int main()
{
    std::cout << "Hello, World!" << std::endl;
    
    return 0;
}
````

This is a basic "Hello, World!" program in C++.

# Building

To build your C++ program you run the following commands from within the directory containing `CMakeLists.txt` and `main.cpp`. First, you generate a build system using CMake's build system generator "Unix Makefiles" by running:

````
cmake -G "Unix Makefiles" .
````

You then execute the generated build system by running:

````
cmake --build .
````

This is it! You are now free to write C++ and build it for both Windows and Linux. Next, we'll get into using (and building) libraries.

# Feedback

If you encounter any issues while following this tutorial, feel free to open an issue!
