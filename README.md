# polybar-dwm-module
![DWM
Module](https://github.com/mihirlad55/polybar-dwm-module/blob/master/dwm-module.png)

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
- Labels:
    * Display dwm tags
        - Separator label between tags
    * Display the current layout
    * Display the currently focused window title (per monitor)
    * Display label when focused window is floating
- Click Handlers:
    * Tags:
        - Left-click tag to view tag
        - Right-click tag to toggle view on tag
    * Layout:
        - Left-click to set `secondary-layout` (specified in config)
        - Right-click to set previous layout
        - Scroll to cycle through layouts (with wrapping and reverse scroll)
- Different formatting for different tag states:
    * Focused: selected tag on selected monitor
    * Unfocused: selected tag on unselected monitor
    * Visible: unselected, but occupied tag on any monitor
    * Urgent: Unselected tag with window that has the urgent hint set
    * Empty: Unselected and unoccupied tags
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
If your polybar is to be displayed on the bottom of the monitor, set `topbar`
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
$ cd polybar-dwm-module
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


## Sample Module Configuration
```ini
...

modules-left = ... dwm ...

...

type = internal/dwm
format = <label-tags> <label-layout> <label-floating> <label-title>

; Left-click to view tag, right-click to toggle tag view
enable-tags-click = false
; Left-click to set secondary layout, right-click to switch to previous layout
enable-layout-click = false
; Scroll to cycle between available layouts
enable-layout-scroll = false
; Wrap when scrolling and reaching begining/end of layouts
layout-scroll-wrap = false
; Reverse scroll direction
layout-scroll-reverse = false

; If enable-layout-click = true, clicking the layout symbol will switch to this layout
secondary-layout-symbol = [M]

; Separator in between shown tags
; label-separator = |

; Title of currently focused window
; Available tokens:
;   %title%
label-title = %title%
label-title-padding = 2
label-title-forefround = ${colors.primary}
label-title-maxlen = 30

; Symbol of current layout
; Available tokens:
;   %symbol%
label-layout = %symbol%
label-layout-padding = 2
label-layout-foreground = #000
label-layout-background = ${colors.primary}

; Text to show when currently focused window is floating
label-floating = F

; States: focused, unfocused, visible, urgent, empty
; Available tokens:
;   %name%

; focused = Active tag on focused monitor
label-focused = %name%
label-focused-background = ${colors.background-alt}
label-focused-underline= ${colors.primary}
label-focused-padding = 2

; unfocused = Inactive tag on any monitor
label-unfocused = %name%
label-unfocused-padding = 2

; visible = Active tag on unfocused monitor
label-visible = %name%
label-visible-background = ${self.label-focused-background}
label-visible-underline = ${self.label-focused-underline}
label-visible-padding = ${self.label-focused-padding}

; urgent = Tag with urgency hint set
label-urgent = %name%
label-urgent-background = ${colors.alert}
label-urgent-padding = 2

; empty = Tags with no windows assigned
; This can be set to an empty string to hide empty tags
label-empty = %name%
label-empty-background = ${colors.primary}
label-empty-padding = 2
```


## License
Polybar is licensed under the MIT license. [See LICENSE for more
information](https://github.com/polybar/polybar/blob/master/LICENSE).
