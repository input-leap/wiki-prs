## Binaries Built

- `input-leap` the GUI front-end and "main" program
- `input-leaps` the CLI server component
- `input-leapc` the CLI client component

**Note**: these aren't the only things built at compile time, but merely what the end-user is expected to use.

## Preparing your system

### Ubuntu/Debian/Raspbian

```shell
sudo apt update && sudo apt upgrade
sudo apt install git cmake make xorg-dev g++ libcurl4-openssl-dev \
                 libavahi-compat-libdnssd-dev libssl-dev libx11-dev \
                 qttools5-dev qtbase5-dev libice-dev libsm-dev
```

### Fedora

(Since Fedora 35, there have been package renames. We leave this to the user, as
versions of Fedora <= F35 are now EOL, and we're not obligated to support EOL
versions of Fedora. The following instructions are known to work on F37.)

```shell
sudo dnf install git cmake make gcc-c++ xorg-x11-server-devel \
                 libcurl-devel avahi-compat-libdns_sd-devel \
                 libXtst-devel qt5-qtbase qt5-qtbase-devel  \
                 qt5-qttools-devel libICE-devel libSM-devel \
                 openssl-devel libXrandr-devel libXinerama-devel
```

### CentOS 8+

(Make sure you have RPM Fusion and EPEL enabled, with PowerTools as well)

```shell
sudo dnf groupinstall "Development Tools"
sudo dnf install 'dnf-command(config-manager)'
sudo dnf config-manager --set-enabled PowerTools
sudo dnf install cmake3 avahi-compat-libdns_sd-devel libX11-devel libXtst-devel \
                qt5-qtbase-devel libcurl-devel desktop-file-utils openssl-devel
```

### openSUSE

```shell
sudo zypper install --type pattern devel_basis
sudo zypper install libdrm-devel libglvnd-devel libICE-devel \
        libQt5Core-devel libQt5Gui-devel libQt5Network-devel \
        libqt5-qtbase-common-devel libQt5Widgets-devel libSM-devel \
        libXinerama-devel libXrandr-devel libXrender-devel
```

## Building from source

```shell
git clone https://github.com/input-leap/input-leap.git
# This builds from master, but you can also checkout a tag or branch.
cd input-leap
git submodule update --init --recursive
./clean_build.sh
sudo cmake --install build # install to /usr/local/
```

### Wayland dependencies
(assumes an Ubuntu OS) For Wayland support, `libportal` must be installed from source, since the package version doesn't have `InputCapture` support yet.  This guide is useful in building it from source:
https://discussion.fedoraproject.org/t/input-leap-fedora-39-gnome-wayland/95856
(Tip for installing packages required for `libportal` build is to use `apt-file search [MISSING_DEPENDENCY]` to locate the correct package to install).

You may need to install:
```shell
sudo apt install python3-jinja2 python3-pygments python3-typogrify libgirepository-1.0-dev valac libgirepository-1.0-dev libgirepository1.0-dev
```

Once `libportal` has been built and installed from source, the following packages must be installed:
```shell
sudo apt install libei-dev
```

Edit `clean_build.sh` and add the lines

```shell
# added for Wayland
B_CMAKE_FLAGS="${B_CMAKE_FLAGS} -DINPUTLEAP_BUILD_LIBEI=TRUE"
```

Run `./clean_build.sh` to build
