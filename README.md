# polybar-dwm-module
**polybar-dwm-module** is a fork of
[polybar](https://github.com/polybar/polybar) which implements a dwm module.
This module requires that dwm have the [IPC
patch](https://github.com/mihirlad55/dwm-ipc). This module uses the
[dwmipcpp](https://github.com/mihirlad55/dwmipcpp) C++ client library for
communicating with dwm (included as a submodule).


## The DWM Module
The dwm module currently supports the following:
- Display dwm tags
- Display the current layout
- Display the currently focused window title (per monitor)
- Left-click to view tag
- Right-click to toggle view on tag
- Pin all tags to bar, or only show occupied/selected tags
- Different formatting for different tag states:
    * Focused: selected tag on selected monitor
    * Unfocused: selected tag on unselected monitor
    * Visible: unselected, but occupied tag on any monitor
    * Urgent: Unselected tag with window that has the urgent hint set
- Separator label between tags
- The combined power of polybar


## License
Polybar is licensed under the MIT license. [See LICENSE for more
information](https://github.com/polybar/polybar/blob/master/LICENSE).
