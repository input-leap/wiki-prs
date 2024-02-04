## FAQ - Frequently Asked Questions

** Q: Input Leap vs. Barrier? **

> A: Input Leap is a fork of barrier, by **barrier's active maintainers**. See [issue #1414](https://github.com/input-leap/input-leap/issues/1414)
>    for more details. Currently, barrier is considered unmaintained.

** Q: Does drag and drop work on Linux? **

> A: No *(see [#855](https://github.com/input-leap/input-leap/issues/855) if you'd like to change that)*

** Q: What OSes are supported? **

Currently, Input Leap is in heavy development, and we hope to make our first
post-fork release very soon. However, we wish to make clear that building from
Git is prone to breaking changes and other bugs/issues. Our advice is to stick
with Barrier v2.4.0/v2.3.4 for the time-being.

<!-- TODO: Update upon v3.0.0 release.
> A: The [most recent release](https://github.com/input-leap/input-leap/releases/latest) of Input Leap is known to work on:
>  - Windows 7, 8, 8.1, 10, and 11
>  - macOS *(previously known as OS X or Mac OS X)*
>    - _The current GUI does **not** work on OS versions prior to macOS 10.12 Sierra (but see the related answer below)_
>  - Linux
>  - FreeBSD
>  - OpenBSD
-->

<!-- TODO: Update upon v3.0.0 release.
**Q: Are 32-bit versions of Windows supported?**

> A: Not officially.
-->

<!-- TODO: Update upon v3.0.0 release.
__Q: Is it possible to use Input Leap on Mac OS X / OS X versions prior to 10.12?__

> A: Not officially.
>   - For OS X 10.10 Yosemite and later:
>     - [Input Leap v2.1.0](https://github.com/input-leap/input-leap/releases/tag/v2.1.0) or earlier _may_ work.
>   - For Mac OS X 10.9 Mavericks _(and perhaps earlier)_:
>     1. the command-line portions of the [current release](https://github.com/input-leap/input-leap/releases/latest) _should_ run fine.
>     2. The GUI will _not_ run, as that OS version does not include Apple's *Metal* framework.
>         - _(For a GUI workaround for Mac OS X 10.9, see the [discussion at issue #544](https://github.com/input-leap/input-leap/issues/544))_

> Note: Only versions [v2.3.4](https://github.com/input-leap/input-leap/releases/tag/v2.3.4) and [later](https://github.com/input-leap/input-leap/releases/latest) of Input Leap can be supported by this project.
>  - Anyone using an earlier version is advised to upgrade due to recently-addressed security vulnerabilities *(and other bug fixes)*.
>    - This is especially important for computers accessible from the public Internet *(or from other shared/untrusted networks, such as when using shared WiFi)*.
-->

** Q: How do I load my configuration on startup? **

> A: Start the binary with the argument `--config <path_to_saved_configuration>`

** Q: After loading my configuration on the client, the field 'Server IP' is still empty! **

> A: Edit your configuration to include the server's ip address manually with
>
>```
>(...)
>
>section: options
>    serverhostname=<AAA.BBB.CCC.DDD>
>```

** Q: Are there any other significant limitations with the current version of Input Leap? **

> A: Currently:
>    - Input Leap currently has limited UTF-8 support; issues have been reported with processing various languages.
>      - *(see [#860](https://github.com/input-leap/input-leap/issues/860))*
>
>    - There is interest in future support for the Wayland compositor/display server protocol *([official site](https://wayland.freedesktop.org/) | [Wikipedia article](https://en.wikipedia.org/wiki/Wayland_(display_server_protocol)))* on Linux.
>      - As of mid-2022, there is no expected completion date for *Wayland* support.
>      - *(see [#109](https://github.com/input-leap/input-leap/issues/109) and [#1251](https://github.com/input-leap/input-leap/issues/1251) for status or to volunteer your talents)*
>
> The complete list of open issues can be found in the ['Issues' tab on GitHub](https://github.com/input-leap/input-leap/issues?q=is%3Aissue+is%3Aopen). Help is always appreciated.
