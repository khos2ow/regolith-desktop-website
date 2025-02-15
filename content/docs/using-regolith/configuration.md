---
title: "Configuration"
linkTitle: "Configuration"
weight: 4
description: >
  Make changes to the way Regolith looks and behaves.
---

## Configuration

--- 

## Wallpaper

Wallpaper can be set by specifying the path to the wallpaper image via the Xresources key `regolith.wallpaper.file`.  

Example, assuming the file `/usr/share/backgrounds/hardy_wallpaper_uhd.png` is present: 

```console
$ echo "regolith.wallpaper.file: /usr/share/backgrounds/hardy_wallpaper_uhd.png" >> ~/.config/regolith2/Xresources
$ regolith-look refresh 
```

To specify a color rather than an image use the Xresource key `regolith.wallpaper.color.primary`:

```console
$ echo "regolith.wallpaper.file: " >> ~/.config/regolith2/Xresources
$ echo "regolith.wallpaper.color.primary: blue" >> ~/.config/regolith2/Xresources
$ regolith-look refresh 
```

To specify a secondary color and gradient:

```console
$ echo "regolith.wallpaper.file: " >> ~/.config/regolith2/Xresources
$ echo "regolith.wallpaper.color.primary: blue" >> ~/.config/regolith2/Xresources
$ echo "regolith.wallpaper.color.secondary: green" >> ~/.config/regolith2/Xresources
$ echo "regolith.wallpaper.color.shading.type: vertical" >> ~/.config/regolith2/Xresources
$ regolith-look refresh 
```


### Disable Wallpaper handling

If you wish to manage wallpaper externally to Regolith, simply specify empty values for wallpaper image and color:

```console
$ echo "regolith.wallpaper.file: " >> ~/.config/regolith2/Xresources
$ echo "regolith.wallpaper.color.primary: " >> ~/.config/regolith2/Xresources
```

## Status Bar Indicators

Status indicators such as CPU load, date and time, notifications, weather, and other system info can be added or removed by installing packages. For example, to show a status indicator for your laptop battery, simply run `sudo apt install i3xrocks-battery` and then refresh the session using `regolith-look refresh`. To find what indicators are available, run `apt search ^i3xrocks-` or search for `i3xrocks-` in your favorite package manager GUI, such as [Synaptic](https://help.ubuntu.com/community/SynapticHowto). There is [more documentation available]({{< ref "/docs/howtos/add-remove-blocklets.md" >}}) for configuring status indicators, also called "blocklets".

{{< img "images/regolith-screenshot-synaptic-search.png" "Searching for blocklets in Synaptics" >}}

## Looks

Colors, wallpaper, window and bar layouts and other visual factors are bundled together in Regolith and called "looks". Looks provide a simple way of changing the entire look of the desktop. Like status bar indicators, looks are packaged and are installed and removed like any other software package. By convention, Look packages use the following naming format `regolith-look-<name>`. `apt` or a GUI package manager can be used to search for available looks. The terminal command `regolith-look` can be used to change looks and refresh the active session with the selected look. Here's an example that switches to the `gruvbox` look:

```console
$ apt search ^regolith-look-
[...]
regolith-look-gruvbox/unknown,now 0.4.6-1regolith amd64
[...]
$ sudo apt install regolith-look-gruvbox
$ regolith-look set gruvbox
$ regolith-look refresh
```

Installed Looks may also be set via the Look Dialog, activated via {{< keys "super,alt,l" >}}.

{{< hint danger >}}
NOTE: Regolith 1.x looks are not compatible with Regolith 2.  As of Regolith 2 Beta 1 release, the following looks are available:

* blackhole
* default
* gruvbox
* nord

{{< /hint >}}

## i3 Features

Starting with Regolith 2.0, many i3 configuration tasks can be configured via the package manager.  i3 `4.20` introduced the ability to specify include files as part of the configuration.  Regolith provides i3 include files in small packages.  By installing and removing packages, i3 configuration can be customized for specific preferences while still allowing to track upstream changes for aspects of the configuration that need not vary.  By default, when the `regolith-desktop` package is installed, these configuration elements are also installed as soft dependencies:

Default i3 Configuration in Regolith Desktop 2

| Package                      | Function          |
|------------------------------|-------------------|
| regolith-i3-base-launchers   | Launch terminal and browser | 
| regolith-i3-default-style    | Window behavior |
| regolith-i3-navigation       | Navigation keybindings |
| regolith-i3-networkmanager   | Network and wifi functions |
| regolith-i3-next-workspace   | Workspace utility |
| regolith-i3-resize           | Resize keybindings |
| regolith-i3-session          | Session keybindings |
| regolith-i3-unclutter        | Hide mouse cursor when unused |
| regolith-i3-user-programs    | Optionally launch user programs specified in Xresources |
| regolith-i3-workspace-config | Workspace keybindings |

Soft dependencies can be removed without causing packages that depend upon it to be removed. This means that any of the listed packages can be removed.  Users can make tweaks to configuration in a more stable manner by replacing a default configuration partial with their own version.  This can be achieved by copying the partial to be customized into `~/.config/regolith2/i3/config.d/` and removing the original via apt.  For example, to customize Workspace keybindings:

```console
$ mkdir -p ~/.config/regolith2/i3/config.d
$ cp /usr/share/regolith/i3/config.d/40_workspace-config ~/.config/regolith2/i3/config.d/
$ vim ~/.config/regolith2/i3/config.d/40_workspace-config # make desired changes
$ sudo apt remove regolith-i3-workspace-config # removes the default version
$ # restart i3 or log back in
```

### All i3 Configuration Packages

The following contains a list of all i3 configuration packages available in Regolith 2.0:

| Package                      | Function          |
|------------------------------|-------------------|
| regolith-i3-base-launchers   | Launch terminal and browser | 
| regolith-i3-compositor       | Compositor integration (delegates to `regolith-compositor-<variant>`) |
| regolith-i3-default-style    | Window behavior |
| regolith-i3-ftue             | First time user experience |
| regolith-i3-gaps-partial     | `i3-gaps` configuration (if installed, i3-gaps will replace i3) |
| regolith-i3-gnome            | Regolith Settings keybindings |
| regolith-i3-i3xrocks         | i3 bar status indicators configuration |
| regolith-i3-ilia             | `ilia` integration |
| regolith-i3-navigation       | Navigation keybindings |
| regolith-i3-networkmanager   | `network-manager` integration |
| regolith-i3-next-workspace   | Auto create next workspace feature |
| regolith-i3-remontoire       | Legacy keybindings view integration |
| regolith-i3-resize           | Resize keybindings |
| regolith-i3-rofi             | Legacy desktop launcher integration |
| regolith-i3-rofication       | Legacy notification viewer integration |
| regolith-i3-rofication-ilia  | Notification viewer integration |
| regolith-i3-session          | Session keybindings |
| regolith-i3-snapshot         | i3 workspace persistence|
| regolith-i3-unclutter        | Hides mouse when not in use |
| regolith-i3-user-programs    | Optionally launch user programs specified in Xresources |
| regolith-i3-workspace-config | Workspace keybindings |

## Keybindings

The most common keybinding change is the {{< keys "super" >}} key. Regolith uses `Xresources` as the canonical source of truth for settings, which are read by various UI components. The table of `Xresources` keys open to user configuration [is available elsewhere]({{< ref "xresources" >}}). To change the default {{< keys "super" >}} binding from the "windows" key to "alt", add the following line to the file `~/.config/regolith2/Xresources`:

```toml
i3-wm.mod: Mod1
i3-wm.alt: Mod4
```

**Note**: GNOME also has it's own set of keybindings. When the Regolith session is first initialized, the conflicting GNOME keybindings are removed from the user settings. GNOME keybindings can be managed in the Regolith Settings app.

{{< img "images/regolith-screenshot-settings-keybindings.png" "GNOME keybindings in the settings dialog">}}

## System Mangement

The `regolith-control-center` app is the tool to configure locale, date, displays, networking and various other settings. Launch it via the app launcher with {{< keys "super,space" >}}, type `settings`, and hit enter to launch the app. The direct keybinding is {{< keys "super,c" >}}.  The application may also be launched from a terminal with command `regolith-control-panel`.

## Further Reading

To dig deeper, find which [Howtos]({{< ref "howtos" >}}) are available, or read the [Xresources reference]({{< ref "docs/Reference/xresources.md" >}}). Become an i3 power user by reading their [user guide](https://i3wm.org/docs/userguide.html).
