# polybar-dwm-module
**polybar-dwm-module** is a fork of
[polybar](https://github.com/polybar/polybar) which implements a dwm module.


## Requirements
* dwm with the [IPC patch](https://github.com/mihirlad55/dwm-ipc) applied
* [dwmipcpp](https://github.com/mihirlad55/dwmipcpp) C++ client library for
  communicating with dwm (included as a submodule).
* [jsoncpp](https://github.com/open-source-parsers/jsoncpp) for polybar and
  dwmipcpp (required by module).

The [dwm-anybar patch](https://github.com/mihirlad55/dwm-anybar) is optionally
recommended for a better experience. This patch allows dwm to manage polybar and
fixes some weird quirks that you may experience without it.


## The DWM Module
The dwm module currently supports the following:
- Display dwm tags
- Display the current layout
- Display the currently focused window title (per monitor)
- Left-click to view tag
- Right-click to toggle view on tag
- Different formatting for different tag states:
    * Focused: selected tag on selected monitor
    * Unfocused: selected tag on unselected monitor
    * Visible: unselected, but occupied tag on any monitor
    * Urgent: Unselected tag with window that has the urgent hint set
    * Empty: Unselected and unoccupied tags
- Separator label between tags
- The combined power of polybar


## How to Install
First, apply all the patches you want on dwm, saving the IPC patch for last.

Optionally, apply the [dwm-anybar
patch](https://github.com/mihirlad55/dwm-anybar) patch and make sure your
`config.h` contains the following
```
static const int showbar            = 1;        /* 0 means no bar */
static const int topbar             = 1;        /* 0 means bottom bar */
static const int usealtbar          = 1;        /* 1 means use non-dwm status bar */
static const char *altbarclass = "Polybar";     /* Alternate bar class name */
```
If you're polybar is to be displayed on the bottom of the monitor, set `topbar`
to `0`.

Next, apply the [IPC patch](https://github.com/mihirlad55/dwm-ipc). There will
likely be merge conflicts. The IPC patch is mostly additive, so in most conflict
cases, you will be keeping both changes.

After appling all your patches, make sure you compile and install dwm
```
$ sudo make install
```

Make sure you have `jsoncpp` installed, and any other requirements from
[polybar](https://github.com/polybar/polybar).

Clone, make, and install polybar. Follow the on screen prompts in the `build.sh`
script and enable any additional features you want.
```
$ git clone https://github.com/mihirlad55/polybar-dwm-module
$ cd polybar
$ ./build.sh -d
```

Configure the bar!  You can view `/usr/share/doc/polybar/config` for a sample config that
includes the supported settings for the dwm module.

**IF YOU APPLIED THE ANYBAR PATCH**, make sure you have
`override-redirect = false` in your polybar config.

**IF YOU DID NOT APPLY THE ANYBAR PATCH**, make sure you have
`override-redirect = true` in your polybar config. You will have to set the bar
height in your dwm's `config.h` to match polybar's height and make sure
`showbar` is set to `1` in your `config.h`. Also make sure `topbar` is set to
the correct value based on if your polybar is a bottom/top bar.


## License
Polybar is licensed under the MIT license. [See LICENSE for more
information](https://github.com/polybar/polybar/blob/master/LICENSE).
