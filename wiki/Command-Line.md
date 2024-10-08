<a name="top"></a>

# Using Input Leap from the Command Line

You might to use the command line without the GUI to run input leap, especially if
you do not change settings frequently or do not want the Qt GUI running all the
time. These instructions cover using Input Leap via the command line interface.

_The [Synergy wiki](https://github.com/symless/synergy-core/wiki) was
used as a reference in creating this documentation._

## Document Conventions

- Text in angle brackets `<text>` is input supplied by the user
- Text in square brackets `[text]` represents optional inputs
- Text in curly braces with pipes `{true|false}` represents options to choose
from
- Text in _italics_ are user interface elements or items on-screen
- Text in a `monospaced font` are keyboard shortcuts, prompts, commands, or
command output

## Topics

- [Windows](#windows)
- [MacOS](#macos)
- [Linux](#linux)
- [Server Command Line Options](#server_cli)
- [Client Command Line Options](#client_cli)
- [Systemd Service](#systemd)
- [Launchd Service](#launchd)
- [Windows Service](#windows_service)
- [Text File Configuration](#text_config)
- [Server Configuration File](#server_config)
- [SSL/TLS Configuration](#ssl_config)

---

## <a name="windows">Windows</a>

To use Input Leap commands from the command line in Windows you can either change
directories to the folder that they are located in each time or add the Input Leap
directory to your `%PATH%` variable.

To change to the directory:

```cmd
cd "\Program Files\Input Leap"
```

To add the directory to `%PATH%`:

- Press `(⊞ Win) + Break` to view the _System_ control panel
- Click on _Advanced system settings_ on the left panel
- On the _Advanced_ tab, click the _Environment Variables..._ button
- In the _System variables_ list, double-click the _Variable_ named _Path_
- Click _New_ and enter `C:\Program Files\Input Leap`
- Click _OK_ in the _Edit environment variable_ dialog
- Click _OK_ in the _Environment Variables_ dialog
- Click _OK_ in the _System Properties_ dialog

This will only effect command prompts opened after the change.

### Portable

The command line version of Input Leap is a single client executable `input-leapc.exe`
and a single server executable `input-leaps.exe`. They both have a dependency to OpenSSL
libraries, `libeay32.dll` and `ssleay32.dll` (used for encryption, unless argument
`--disable-crypto`), as well as Microsoft Visual C++ runtime libraries.

From an existing installation you can copy the necessary program files to
a location of choice, to get a command line only portable (depending on configuration)
installation. It is also possible to extract the files directly from the installer
by using the tool [innounp](http://innounp.sourceforge.net/).
Copy the following files from the installation directory `C:\Program Files\Input Leap`:

```
input-leapc.exe
input-leaps.exe
libeay32.dll
ssleay32.dll
```

As long as you have the
[Microsoft Visual C++ Redistributable for Visual Studio 2019](https://visualstudio.microsoft.com/downloads/)
installed (or copy the necessary runtime libaries `msvcp140.dll`, `vcruntime140.dll` and
`vcruntime140_1.dll` into the application directory), you will now have a stand-alone
application directory that you can manually copy into computers where you need it.

To be able to generate server certificate used for encryption, you may need a separate
OpenSSL installation (on the server).

For a completely portable installation, with local configuration, you must configure the
location of server configuration file and SSL/TLS configuration files. See
[Text File Configuration](#text_config), [Server Command Line Options](#server_cli),
[Client Command Line Options](#client_cli) and [SSL/TLS Configuration](#ssl_config), below.

<a href="#top">Back to top</a>

---

## <a name='macos'>MacOS</a>

To use Input Leap commands from the command line on MacOS you can either change
directories to the folder they are located and run them using the relative path
(i.e. `./input-leaps`) each time or add the `Input Leap.app/Contents/MacOS` directory
to your `$PATH`.

```cmd
cd /Applications/Input Leap.app/Contents/MacOS/
```

To add the directory to `$PATH`:
```cmd
export PATH=/Applications/Input Leap.app/Contents/MacOS/:$PATH
```

The `$PATH` variable will only be set for the duration of the current shell
session. To make the path persistent, add it as a new line in the `/etc/paths`
file or set the `$PATH` variable in your `.profile` or `.bashrc` file.

<a href="#top">Back to top</a>

---

## <a name="linux">Linux/Unix</a>

If Input Leap has been installed using a package manager or equivalent it should
already be in your `$PATH`.

If installed using flatpak, you can run the command line client like this:
```cmd
flatpak run -command=input-leapc io.github.input_leap.InputLeap
```
And server like this:
```cmd
flatpak run --command=input-leaps io.github.input_leap.InputLeap
```

<a href="#top">Back to top</a>

---

## <a name="server_cli">Server Command Line Options</a>

To see the server command line options, use the `--help` argument:
```
input-leaps --help
Start the input-leap server component.

Usage: input-leaps [--address <address>] [--config <pathname>] [--daemon|--no-daemon] [--name <screen-name>] [--restart|--no-restart] [--debug <level>]

Options:
  -a, --address <address>  listen for clients on the given address.
  -c, --config <pathname>  use the named configuration file instead.
  -d, --debug <level>      filter out log messages with priority below level.
                             level may be: FATAL, ERROR, WARNING, NOTE, INFO,
                             DEBUG, DEBUG1, DEBUG2.
  -n, --name <screen-name> use screen-name instead the hostname to identify
                             this screen in the configuration.
  -1, --no-restart         do not try to restart on failure.
      --restart            restart the server automatically if it fails. (*)
  -l  --log <file>         write log messages to file.
      --no-tray            disable the system tray icon.
      --enable-drag-drop   enable file drag & drop.
      --enable-crypto      enable the crypto (ssl) plugin (default, deprecated).
      --disable-crypto     disable the crypto (ssl) plugin.
      --profile-dir <path> use named profile directory instead.
      --drop-dir <path>    use named drop target directory instead.
  -f, --no-daemon          run in the foreground.
```

<a href="#top">Back to top</a>

---

## <a name="client_cli">Client Command Line Options</a>

To see the client command line options, use the `--help` argument:
```
input-leapc --help
Start the input-leap client and connect to a remote server component.

Usage: input-leapc [--yscroll <delta>] [--daemon|--no-daemon] [--name <screen-name>] [--restart|--no-restart] [--debug <level>] <server-address>

Options:
  -d, --debug <level>      filter out log messages with priority below level.
                             level may be: FATAL, ERROR, WARNING, NOTE, INFO,
                             DEBUG, DEBUG1, DEBUG2.
  -n, --name <screen-name> use screen-name instead the hostname to identify
                             this screen in the configuration.
  -1, --no-restart         do not try to restart on failure.
      --restart            restart the server automatically if it fails. (*)
  -l  --log <file>         write log messages to file.
      --no-tray            disable the system tray icon.
      --enable-drag-drop   enable file drag & drop.
      --enable-crypto      enable the crypto (ssl) plugin (default, deprecated).
      --disable-crypto     disable the crypto (ssl) plugin.
      --profile-dir <path> use named profile directory instead.
      --drop-dir <path>    use named drop target directory instead.
  -f, --no-daemon          run in the foreground.
      --daemon             run as a daemon. (*)
```

<a href="#top">Back to top</a>

---

## <a name="systemd">Creating a systemd service (Linux)</a>

[comment]: <> (TODO: This section will need to be updated if PR #694 is merged)

If you would like to add the input leap client or server as a service on a
systemd-based linux distribution, you can create a 
[`.service` file for systemd](https://www.freedesktop.org/software/systemd/man/systemd.service.html).

Running Input Leap as a systemd service as the root user will allow Input Leap to
access any X11 screen. If you need to use Input Leap before logging (i.e. in a
Display Manager like GDM) in this is possibly the only option despite the
possible security concern of running Input Leap as root. If you do not need to use
Input Leap at the login screen it is likely better to run Input Leap under your user
account.

Here is an example `.service` template for a service on a computer used by one
person where Input Leap does not need access to the Display Manager. This can be
put in the `/etc/systemd/system/` directory and started or stopped with the
`systemctl` command. This assumes that the X11 display is on `:0`.

```ini
[Unit]
Description=Input Leap Client daemon
After=network.target

[Service]
User=<username>
Group=<groupname>
ExecStart=input-leapc --enable-crypto --display :0 --debug INFO -f <server hostname or IP>
Restart=always

[Install]
WantedBy=multi-user.target
```

If you want to use a systemd Input Leap service on a multi-user system, consider 
using a [user service](https://www.freedesktop.org/software/systemd/man/user@.service.html)
or starting the GUI application at logon instead.

The input-leap client can also be started from the command line remotely using
`ssh` as long as `$DISPLAY` is set or specified with `--display`.

<a href="#top">Back to top</a>

---

## <a name="launchd">Launchd daemon (MacOS)</a>

If you want to create a daemon for MacOS instead of using the GUI, you can 
create a daemon/agent using a `.plist` file in `~/Library/LaunchAgents`. 
Information about creating daemons/agents for MacOS can be found at 
[launchd.info](https://www.launchd.info/).

The recommended method of starting automatically on MacOS is with the GUI by
dragging _Input Leap.app_ to the _Login Items_ pane in _System Preferences_ >
_Users & Groups_. This method does start Input Leap after logging in.

<a href="#top">Back to top</a>

---

## <a name="windows_service">Windows Service</a>

The Windows version uses a service that can be started/stopped in the Windows
[Services snap-in](https://en.wikipedia.org/wiki/Windows_service#Services_snap-in).
The Services snap-in can be accessed by pressing `(⊞ Win) + R` and typing
`services.msc` in the _Run_ dialog. The service is named `Input Leap`.

<a href="#top">Back to top</a>

---

## <a name="text_config">Text File Configuration</a>

If you use Input Leap from the command line you may need to create a configuration
file. Configuration files can be copied from their default GUI locations as a
baseline.

The client will use the configuration specified by the server.

By default the server will look for a configuration file at the following paths, in prioritized order:
- User specific location: `%LocalAppData%\Input Leap\InputLeap.sgc` on Windows, `$XDG_DATA_HOME/.config/InputLeap/InputLeap.conf` on Linux.
- System shared location: `C:\ProgramData\Input Leap\InputLeap.sgc` on Windows, `/etc/InputLeap.conf` on Linux.

The user specific location can be customized with command line argument `--profile-dir`,
and Input Leap will look for a configuration file with default name (`InputLeap.sgc` on Windows,
`InputLeap.conf` on Linux) there:

```shell
input-leaps --profile-dir ~/input-leap/config/path ...
```

You can also use command line argument `--config` to set path to a specific configuration
file that should be used.

```shell
input-leaps --config ~/input-leap/config/path/file.conf ...
```

<a href="#top">Back to top</a>

---

## <a name="server_config">Server Configuration File</a>

The text file configuration uses four different sections; `screens`, `aliases`,
`links` and `options`. The structure of a server configuration file looks
something like this:

```yaml
section: screens
    hostname1:
        setting = value
    hostname2:
        setting = value
end
section: aliases
    hostname1:
        hostname1.alias
    hostname2:
        hostname2.alias
end
section: links
    hostname1:
        direction = hostname2
    hostname2:
        direction = hostname1
end
section: options
    option = value
end
```

Examples can be found [in the `doc` directory](https://github.com/input-leap/input-leap/tree/master/doc) of the Input Leap repository.

<a href="#top">Back to top</a>

---

### Screen Options

By default screens use the hostname of the server or client. Each screen may
have any of the following settings:
```ini
halfDuplexCapsLock = {true|false}
halfDuplexNumLock = {true|false}
halfDuplexScrollLock = {true|false}
switchCorners = {none, top-left, top-right, bottom-left, bottom-right, left, right, top, bottom, all}
switchCornerSize = N
xtestIsXineramaUnaware = {true|false}
preserveFocus = {true|false}
shift = {shift|ctrl|alt|meta|super|none}
ctrl = {shift|ctrl|alt|meta|super|none}
alt = {shift|ctrl|alt|meta|super|none}
altgr = {shift|ctrl|alt|meta|super|none}
meta = {shift|ctrl|alt|meta|super|none}
super = {shift|ctrl|alt|meta|super|none}
```
- `halfDuplexCapsLock`, `halfDuplexNumLock`, and `halfDuplexScrollLock` are for
clients that use a press to enable and a release to disable instead of toggling
with a press and release
- `switchCorners` prevents switching when reaching the edge of any of the listed
corners
- `switchCornerSize` is the size in pixels to ignore on a screen edge when using
`switchCorners`
- `xtestIsXineramaUnaware` works around a bug when using certain versions of the
XTest extension in combination with Xinerama on X11 clients (Linux)
- `preserveFocus` prevents dropping focus of the current window when switching
screens
- `shift, ctrl, alt, altgr, meta,` and `super` allow these keys to be mapped to
a different key for that screen

<a href="#top">Back to top</a>

---

### Aliases

By default a screen name is the hostname of the client or server. However, the
screen name can be specified on the command line for both the server and client
with the `--screen` option and if there is a matching Alias it will be 
recognized. Aliases must be unique.

<a href="#top">Back to top</a>

---

### Links

The links section describes the screens relationships to each other. Links allow
you to specify how screens are layed in relation to each other. Links use the
following format:
```
{left|right|up|down}(<range>) = name(<range>)
```

Each link defines a screen edge and the screen name it connects to. The range is
an optional percentage (between 0 and 100) of the edge that will connect to the
other screen. For example, if there are two hosts on the right of `host1` and
they are split 50-50 on the right edge, the configuration might look something
like this:

```yaml
section: links
    host1:
        right(0,50) = host2(50,100)
        right(50,100) = host3(0,50)
...
```

Overlaps on the screen ranges are not supported.

A simpler configuration with two hosts might look like this:

```yaml
section: links
    host1:
        right = host2
    host2:
        left = host1
```

The GUI can be used to set up the layout and the configuration can be copied
into the configuration file being used for the command line.

<a href="#top">Back to top</a>

---

### Options

The key/value pairs in the options section are global options that apply to all
screens.
```ini
heartbeat = N
switchCorners = {none, top-left, top-right, bottom-left, bottom-right, left, right, top, bottom, all}
switchCornerSize = N
switchDelay = N
switchDoubleTap = N
switchNeedsShift = {true|false}
switchNeedsControl = {true|false}
switchNeedsAlt = {true|false}
screenSaverSync = {true|false}
relativeMouseMoves = {true|false}
clipboardSharing = {true|false}
clipboardSharingSize = N
win32KeepForeground = {true|false}
keystroke(key) = actions
mousebutton(button) = actions
```

- `heartbeat` disconnects clients if they do not send a message within `N` 
milliseconds
- `switchCorners` prevents switching screens when reaching the edge on any
of the listed corners
- `switchCornerSize` is the size in pixels to ignore on a screen edge when using
`switchCorners`
- `switchDelay` prevents switching unless the mouse rests on the edge for 
`N` milliseconds
- `switchDoubleTap` prevents switching unless the edge is double-tapped 
within `N` milliseconds
- `switchNeedsShift` prevents switching unless the shift key is held
- `switchNeedsControl` prevents switching unless the control key is held
- `switchNeedsAlt` prevents switching unless the alt key is held
- `screenSaverSync` will sync the screensavers if set to `true`. If set to false
the clients will use their own screensaver settings and the server screensaver
won't start as long as there is input to any screen
- `relativeMouseMoves` causes clients to move the mouse using relative 
coordinates rather than absolute when the cursor is locked to a screen. This is
may assist with certain games
- `clipboardSharing` enables sharing clipboard contents between server and
clients if set to `true`
- `clipboardSharingSize` sets a limit of `N` Kb of data when clipboard sharing
is enabled
- `win32KeepForeground` grabs the focus of on a Windows server on switching to a
client if set to `true`. If set to `false` it will leave the current window in
the foreground. Leaving this setting on `true` avoids issues with other apps
interfering with reading hardware inputs
- `keystroke` can be used to bind <a href="#actions">actions</a> to 
<a href="#keys_list">keys</a>
- `mousebutton` can be used to bind a modifier and a mouse button (left is 1,
middle is 2, and right is 3) to an <a href="#actions">action</a>.

<a href="#top">Back to top</a>

---

### <a name="actions">Actions</a>

<a href="#top">Back to top</a>

---

### <a name="keys_list">Keys</a>

Keys can be in either unicode hexadecimal format (i.e. `\uXXXX`) or a valid key
name. The following named keys are valid in a configuration:

| Standard Keys | Standard Keys | Keypad Keys    | Media Keys | Web Keys     |
|---------------|---------------|----------------|------------|--------------|
| F1 to F35     | Left          | KP_0 to KP_9   | AppMail    | WWWBack      |
| Ampersand     | LeftTab       | KP_F1 to KP_F4 | AppMedia   | WWWFavorites |
| Apostrophe    | Less          | KP_Add         | AppUser1   | WWWForward   |
| Asterisk      | Linefeed      | KP_Begin       | AppUser2   | WWWHome      |
| At            | Menu          | KP_Decimal     | AudioDown  | WWWRefresh   |
| BackSpace     | Minus         | KP_Delete      | AudioMute  | WWWSearch    |
| Backslash     | NumLock       | KP_Divide      | AudioNext  | WWWStop      |
| Bar           | Number        | KP_Down        | AudioPlay  |              |
| Begin         | PageDown      | KP_End         | AudioPrev  |              |
| BraceL        | PageUp        | KP_Enter       | AudioStop  |              |
| BraceR        | ParenthesisL  | KP_Equal       | AudioUp    |              |
| BracketL      | ParenthesisR  | KP_Home        | Eject      |              |
| BracketR      | Pause         | KP_Insert      |            |              |
| Break         | Percent       | KP_Left        |            |              |
| Cancel        | Period        | KP_Multiply    |            |              |
| CapsLock      | Plus          | KP_PageDown    |            |              |
| Circumflex    | Print         | KP_PageUp      |            |              |
| Clear         | Question      | KP_Right       |            |              |
| Colon         | Redo          | KP_Separator   |            |              |
| Comma         | Return        | KP_Space       |            |              |
| Delete        | Right         | KP_Subtract    |            |              |
| Dollar        | ScrollLock    | KP_Tab         |            |              |
| DoubleQuote   | Select        | KP_Up          |            |              |
| Down          | Semicolon     |                |            |              |
| End           | Slash         |                |            |              |
| Equal         | Sleep         |                |            |              |
| Escape        | Space         |                |            |              |
| Exclaim       | Space         |                |            |              |
| Execute       | SysReq        |                |            |              |
| Find          | Tab           |                |            |              |
| Grave         | Tilde         |                |            |              |
| Greater       | Underscore    |                |            |              |
| Help          | Undo          |                |            |              |
| Home          | Up            |                |            |              |
| Insert        |               |                |            |              |

<a href="#top">Back to top</a>

----

## <a name="client_config">Client Configuration File</a>

Client options are set either by the command line arguments or by the server the
client has connected to. There is no `--config` argument for the `input-leapc`
client command.

The client saves a configuration file that can be read for informational or
troubleshooting purposes, and is structured like an `.ini` file. It has two
sections, `[General]` and `[internalConfig]`.

<a href="#top">Back to top</a>

## <a name="ssl_config">SSL/TLS Configuration</a>

Input Leap supports SSL/TLS encryption, by use of the `OpenSSL` library (included).
Starting with version 2.4.0 this is enabled by default, but requires a certificate
and fingerprint.

The SSL related configuration is kept in subdirectory "SSL" in the same user specific location
as the [text file configuration](#text_config) is loaded from: By default
`%LocalAppData%\Input Leap\SSL` on Windows, `~/.local/share/InputLeap/SSL` or `$XDG_DATA_HOME/.config/InputLeap/SSL`
on Linux, but configurable with command line argument `--profile-dir`.

On the server, the root of the SSL directory must contain the certificate as a file
with name `Input Leap.pem`, containing the private and public key.

Input Leap uses fingerprints to validate that a malicious server is not trying to intercept
a client connection, and be if successfull it would be able to send mouse and keyboard
input to the client. A server's fingerprint must be generated from the certificate, and
may be kept in file `SSL/Fingerprints/Local.txt` on the server. All clients must have the
fingerprint hash string of trusted servers in a file `SSL/Fingerprints/TrustedServers.txt`.
When connecting to a server, if it presents a fingerprint not explicitely trusted by the
client, it will refuse the connection. See also
[Fingerprint trust troubleshooting](https://github.com/input-leap/input-leap/wiki/Troubleshooting#fingerprint-trust).

The server will therefore typically contain the following files:
```
/SSL/Input Leap.pem
/SSL/Fingerprints/Local.txt
```

Clients must contain the following file:
```
/SSL/Fingerprints/TrustedServers.txt
```

In addition to the above described server identify verification on clients, Input Leap also
supports verification of client identities connecting to the server. This is not as
critical as the verification of server identity, since a malicous client will not be able
to control the mouse and keyboard on server, but it can still receive input and
potentially set the clipboard etc. In the main UI application this is disabled by default,
but can be activated with setting "Require client certificate". When running server from
command-line it is the opposite: Enabled by default, but can be disabled with command-line
argument `--disable-client-cert-checking`. When this is enabled the client also needs a
certificate, same as server, and its fingerprint must be added to file
`SSL/Fingerprints/TrustedClients.txt` on the server.

The server will now contain the following files:
```
/SSL/Input Leap.pem
/SSL/Fingerprints/Local.txt
/SSL/Fingerprints/TrustedClients.txt
```

Clients will now contain the following files:
```
/SSL/Input Leap.pem
/SSL/Fingerprints/Local.txt
/SSL/Fingerprints/TrustedServers.txt
```


### Generating certificate and fingerprint

The main UI application has built-in functionality for handling encryption.
On first start it will generate a self-signed server certificate and save to disk,
together with a copy of its fingerprint. In client mode it will prompt for you to accept
the server's fingerprint, and add it to your list of trusted servers. If setting
"Require client certificate" is enabled it will also in server mode prompt to accept
clients fingerprints, and add it to the list of trusted clients.
In a command line only ([portable](#portable)) environment you will have to handle
this fingerprint trust manually.

To manually create the certificate and fingerprint similar to how the UI application does
it, you can follow the Windows example below. It creates them in the default location
`%LocalAppData%\Input Leap\SSL`. If you have the are planning to keep the SSL files in a
custom location specified with command line argument `--profile-dir`, you must change
the paths in the example accordingly. It also requires an OpenSSL installation,
e.g installer from [http://slproweb.com/products/Win32OpenSSL.html] installed into
default location `C:\Program Files\OpenSSL-Win64`.

```
MKDIR "%LocalAppData%\Input Leap\SSL\Fingerprints" >NUL 2>&1
"C:\Program Files\OpenSSL-Win64\bin\openssl.exe" req -config "C:\Program Files\OpenSSL-Win64\bin\openssl.cfg" -x509 -nodes -days 365 -subj /CN=Input Leap -newkey rsa:2048 -keyout "%LocalAppData%\Input Leap\SSL\Input Leap.pem" -out "%LocalAppData%\Input Leap\SSL\Input Leap.pem"
FOR /F "tokens=2 delims=^=" %%a in ('""C:\Program Files\OpenSSL-Win64\bin\openssl.exe" x509 -fingerprint -sha256 -noout -in "%LocalAppData%\Input Leap\SSL\Input Leap.pem""') DO ECHO v2:sha256:%a> "%LocalAppData%\Input Leap\SSL\Fingerprints\Local.txt"
```

Now, on any clients you must manually ensure there is a text file
`%LocalAppData%\Input Leap\SSL\Fingerprints\TrustedServers.txt`,
and append the line from the text file
`%LocalAppData%\Input Leap\SSL\Fingerprints\Local.txt` on server,
e.g.

```
v2:sha256:92:D0:AB:DD:38:5C:E5:21:20:8E:52:E8:83:28:A0:2A:CC:CC:8F:A3:70:41:9B:A6:D7:98:9C:ED:50:3F:D7:FE
```

When using client verification you must also do the same the other way around:
copy the fingerprint from `%LocalAppData%\Input Leap\SSL\Fingerprints\Local.txt` on each
client into `%LocalAppData%\Input Leap\SSL\Fingerprints\TrustedClients.txt` on server.

---
