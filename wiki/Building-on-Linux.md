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
                 libqt5-dev qtbase5-dev
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
cd build
sudo make install # install to /usr/local/
```
