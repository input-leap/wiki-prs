# Overview

## Before You Start

You should be at least moderately comfortable with Git, CMake, and the command
line before relying on this method. It requires a good bit of free hard drive
space due to Visual Studio and Qt being required to build. When in doubt go for [binaries](Home) instead!

## Preparing your system
Make sure you install these before you build.


  - [Visual Studio Community](https://visualstudio.microsoft.com/vs/community/) development with C++
  - [CMake](https://cmake.org/download/)
    - can install via the Qt installer
  - [Qt (Open Source)](https://www.qt.io/download)
    - on the select components screen, check the Qt version you want, for example, `6.x.x`, `x` being the latest.
  - [mDNSResponder](https://github.com/nelsonjchen/mDNSResponder/releases/download/v2019.05.08.1/x64_RelWithDebInfo.zip)
  - openssl 1.1.1+
    - can install from via Qt installer
  - git


## Clone the repository

If you don't already have the code, you can check out the code using git. This will make a folder input-leap that contains the code.

    git clone --recurse-submodules https://github.com/input-leap/input-leap.git

Make sure you get the submodules or the you will not be able to build.

## Building from source

Building on windows (and really any os) is made of two parts. Both of these commands are run from the root of the input-leap source code from the visual studio command line
 First Configuration (-S is where the source is and -B is where to put the build generated stuff). You may want to set additional [Build-Options].

 If you see errors saying its unable to find some_ROOT or soemthing_DIR add -DSomething_DIR=file.cmake or -DSomething_ROOT=path to the command below. you will set this to either the location of the foo.cmake file (if its _DIR missing) or the root of the install if its _RooT

    cmake -S. -Bbuild

Then Building  (--build invokes the compiler on the "build" folder we made when we configured)

    cmake --build build --target install --prefix=input-leap-install

 The folder `input-leap-install` will contain the input-leap installation. You will want to run the input-leap.exe in that folder.


[Build-Options]:Build-Options.md

