## Input Leaps Configuration Options
input-leap Supports Several Build options
If you are running cmake from the command line use the switch -DOption=Value when when you configure.

Build Options:
         Option          |            Description                         |   Default Value    | Addtional Requirments |
:-----------------------------:|:----------------------------------------------:|:------------------:|:---------------------:|
CMAKE_BUILD_TYPE               | Type of Build that is produced                 | Release            | |
INPUTLEAP_BUILD_GUI            | Build the Gui                                  | ON                 | Qt|
QT_DEFAULT_MAJOR_VERSION       | Version of Qt to use for gui  (5 or 6)         | 6                  | Must Build Gui For any Effect |
INPUTLEAP_BUILD_TESTS          | Builds inputleap tests                         | ON                 | |
INPUTLEAP_BUILD_EXTERNAL_GTEST | Use System Google Test for test building       | OFF                | gmock and gtest on your system |
INPUTLEAP_BUILD_X11            | XWindows support (required) (linux only)       | ON                 | xorg-devel |
INPUTLEAP_BUILD_LIBEI          | libei support (wayland, flatpak) (linux only)  | OFF                | libei , libportal |
