# Introduction

The goal of this tutorial is to get you set up for building C++ software for both Windows and Linux operating systems. I try to focus on the commonalities between the build processes on each OS. The project file, source code and build commands are the same in both cases.

# Required Tools

* Git
* GCC
* Make
* CMake
* Your text editor of choice

# Windows 11 (MSYS 2)

Install MSYS 2 from https://www.msys2.org/. Install packages:

* git
* mingw-w64-x86_64-gcc
* make
* cmake

````
pacman -S git mingw-w64-x86_64-gcc make cmake
````

# Ubuntu 24.04.2 LTS (WSL)

Set up WSL. Run:

````
wsl --install
````

in PowerShell or Command Prompt. You will have to choose a Distro and set up a user. This tutorial assumes that you chose Ubuntu.

Install packages:

* git
* build-essential (gcc, make)
* cmake

````
sudo apt-get update && sudo apt-get install -y git build-essential cmake
````

# CMakeLists.txt

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

This is your project file. Here you configure the compiler and list your source files, including headers. The first two lines are basically boilerplate. Here you choose which version of CMake you want and the name of your project within your CMake configuration.

Then we require C++ version 17 and add the `-static` flag to avoid as many external dependencies as possible. This flag is a GCC linker option and will not work with other compilers.

Finally, we define an executable from a list of files, in this case only our `main.cpp` file.

# main.cpp

````
#include <iostream>

int main()
{
    std::cout << "Hello, World!" << std::endl;
    
    return 0;
}
````

This is a basic "Hello, World!" program in C++.

# build.sh

````
cmake -G "Unix Makefiles" . && cmake --build .
````

This is all you need to build your CMake project. You will notice that the command has two parts: Configuring and building. Configuring creates a build system for GNU Make and building essentially runs Make in the background.
