# Overview

## Before You Start

You should be at least moderately comfortable with Git, CMake, and the command
line before relying on this method. It requires a good bit of free hard drive
space due to XCode being required to build anything on mac os. When in doubt go for [binaries](Home) instead!

# How to Build InputLeap.app on MacOS

- Install Xcode from the App Store or download and install it
from the [Apple Developer Website](https://developer.apple.com/download/more/?=xcode)
- Install either [MacPorts](https://www.macports.org/) or [Homebrew](https://brew.sh/)
following the instructions on their websites
- Install dependencies with either MacPorts or Homebrew (see below)
- Build either the `Debug` or the `Release` targets (see below)

## Dependencies

You can use either homebrew or macports to get the dependencies
  - cmake
  - openssl
  - qt6

Are required to build

### Install dependencies with Homebrew

  ```
  brew install qt cmake openssl git pkg-config
  ```

### Install dependencies with MacPorts

  ```
  sudo port install qt6 qt6-qttools openssl pkgconfig git cmake
  ```

## Clone the repository
You can check out the code using git. This will make a folder input-leap that contains the code.

    git clone --recurse-submodules https://github.com/input-leap/input-leap.git

Make sure you get the submodules or the you will not be able to build.

## Building the Project
Building on mac os (and really any os) is made of two parts. Both of these commands are run from the root of the input-leap source code.
 First Configuration (-S is where the source is and -B is where to put the build generated stuff). see [Build-Options] for additional options.

    cmake -S. -Bbuild

 Then Building  (--build invokes the compiler on the "build" folder we made when we configured)

    cmake --build build

 The .app will be in build/bundle


## Code signing the .app

If you do not code sign the `.app` inside the bundle folder, a crash
can occur when you try to run it depending on your system
configuration. The crash report will show the `Termination Reason` as:

```
...
Termination Reason:    Namespace CODESIGNING, Code 2 Invalid Page"
...
```

  - Sign the `InputLeap.app` bundle to prevent this crash
  ```
  codesign --force --deep --sign - ./build/bundle/InputLeap.app
  ```

You do not need to have set up a signing identity with apple for this
to prevent the crash.

can occur when you try to run it depending on your system
configuration. The crash report will show the `Termination Reason` as:

```
...
Termination Reason:    Namespace CODESIGNING, Code 2 Invalid Page"
...
```

  - Sign the `InputLeap.app` bundle to prevent this crash
  ```
  codesign --force --deep --sign - ./build/bundle/InputLeap.app
  ```

You do not need to have set up a signing identity with apple for this
to prevent the crash.

[Build-Options]:Build-Options.md
