# Overview

## Before You Start

You should be at least moderately comfortable with Git, CMake, and the command
line before relying on this method. When in doubt go for [binaries](Home) instead!


## Binaries Built

- `input-leap` the GUI front-end and "main" program
- `input-leaps` the CLI server component
- `input-leapc` the CLI client component

**Note**: these aren't the only things built at compile time, but merely what the end-user is expected to use.

## Preparing your system
Make sure you install these before you build. If you get lost you can always check the [github workflow](https://github.com/input-leap/input-leap/blob/master/.github/workflows/builds.yml) to see how we build for your distro. Depending on your distrobution you may need to install `dev` or `devel` packages to get the files need to build against the dependencies.

   - cmake
   - Qt (when building the gui, Qt6 is the default used)
   - xorg-dev files
   - libportal 0.8+ (needed for wayland or flatpak builds)
   - libei (needed for wayland support)
   - avahi
   - openssl 1.1.1+

### Fedora
The following instructions are known to work on F40.

``` shell
sudo dnf install "pkgconfig(avahi-compat-libdns_sd)" "cmake >= 3" "desktop-file-utils" "gcc-c++" \
                 "pkgconfig(x11)" "pkgconfig(xtst)" "pkgconfig(xinerama)" "pkgconfig(xrandr)" "pkgconfig(ice)" \
                 "pkgconfig(sm)" "pkgconfig(openssl)" "pkgconfig(Qt6Core)" "pkgconfig(Qt6Widgets)" \
                 "pkgconfig(Qt6Network)" "pkgconfig(Qt6Linguist)" "make" "pkgconfig(libei-1.0)" "pkgconfig(libportal) >= 0.8" "git"
```



### openSUSE

```shell
sudo zypper install "pkgconfig(avahi-compat-libdns_sd)" "cmake >= 3" "desktop-file-utils" "gcc-c++" \
                    "pkgconfig(x11)" "pkgconfig(xtst)" "pkgconfig(xinerama)" "pkgconfig(xrandr)" "pkgconfig(ice)" "pkgconfig(sm)" \
                    "pkgconfig(openssl)" "pkgconfig(Qt6Core)" "pkgconfig(Qt6Widgets)" \
                    "pkgconfig(Qt6Network)" "pkgconfig(Qt6Linguist)" "make" "pkgconfig(libei-1.0)" "pkgconfig(libportal) >= 0.8" "git"
```

## Clone the repository

If you don't already have the code, you can check out the code using git. This will make a folder input-leap that contains the code.

    git clone --recurse-submodules https://github.com/input-leap/input-leap.git

Make sure you get the submodules or the you will not be able to build.

## Building from source

Building on linux (and really any os) is made of two parts. Both of these commands are run from the root of the input-leap source code.
 First Configuration (-S is where the source is and -B is where to put the build generated stuff). You may want to set additional [Build-Options].

    cmake -S. -Bbuild

Then Building  (--build invokes the compiler on the "build" folder we made when we configured)

    cmake --build build

 The binaries will be in build/bin

### Installing

If you want to install your build you should instead use this build command with out the prefix cmake will want to install into `/usr/local`

    sudo cmake --build build --target install --prefix=/usr`



[Build-Options]:Build-Options.md

