---
label: Linux
order: 998
icon: /static/linux.svg
---

# Emulation on Linux

## Waydroid

!!!success GPU Requirements

Waydroid currently works best with **Intel GPUs**. They should work out of the box.

AMD GPUs appear to have mixed results (in particular, the _RX 6800_ does not work); if Waydroid does _not_ work you might also want to try the NVIDIA instructions below.

NVIDIA GPUs do _not_ work currently, but there are 2 workarounds:

-   Switch to integrated graphic card if possible;
-   Use software rendering:
    -   Make sure that you have already run `waydroid init` (see [#Installation](https://wiki.archlinux.org/title/Waydroid#Installation) section)
    -   Edit `/var/lib/waydroid/waydroid_base.prop` and set:
        
        ```
        ro.hardware.gralloc=default
        ro.hardware.egl=swiftshader
        ```
        
    -   [Restart](https://wiki.archlinux.org/title/Restart "Restart") the `waydroid-container.service`.
!!!
___
## Fedora 36
___

!!!danger
Kernels 5.18.18 to 5.19.5 are broken.
!!!

[!badge variant="light" text="Step 1"] Add the Copr repository

```sh
sudo dnf copr enable aleasto/waydroid
```

[!badge variant="light" text="Step 2"] Install waydroid

```sh
sudo dnf install waydroid
```

When launching waydroid from the application menu you'll be asked to initialize waydroid with some android images. Use the following links:

System OTA: `https://ota.waydro.id/system`

Vendor OTA: `https://ota.waydro.id/vendor`

!!!warning
This will download non-free components (ffmpeg, possibly others).
!!!

___
## Ubuntu 22.04
___

[!badge variant="light" text="Step 1"] Install Pre-requisites

```sh
sudo apt install curl ca-certificates -y
```

[!badge variant="light" text="Step 2"] The Repo

Add the repo to your sources.list (for droidian & ubports, this step can be skipped)
Replace DISTRO="jammy" with your current target. Options: focal, jammy, ubuntu-devel, bookworm, bullseye, sid

```sh
export DISTRO="jammy"
```

```sh
sudo curl --proto '=https' --tlsv1.2 -Sf https://repo.waydro.id/waydroid.gpg --output /usr/share/keyrings/waydroid.gpg && \
echo "deb [signed-by=/usr/share/keyrings/waydroid.gpg] https://repo.waydro.id/ $DISTRO main" > ~/waydroid.list && \
sudo mv ~/waydroid.list /etc/apt/sources.list.d/waydroid.list && \
sudo apt update
```

[!badge variant="light" text="Step 3"] Install Waydroid

```sh
sudo apt install waydroid -y
```

Then start Waydroid from the applications menu.

___
## Install and Run Android Applications
___

Waydroid is able to perform a few various operations found by using the waydroid app -h command:

```
usage: waydroid app [-h] {install,remove,launch,list} ...

optional arguments:
  -h, --help            show this help message and exit

subaction:
  {install,remove,launch,list}
    install             push a single package to the container and install it
    remove              remove single app package from the container
    launch              start single application
    list                list installed applications
```

To launch an app ising CLI, you would want to use the waydroid app launch <appname> command:

```sh
waydroid app launch xyz.apk
```

You can also install Android applications from the command line.

```sh
waydroid app install xyz.apk
```

The apk files you will sometimes find on the internet tend to only have arm support, and will therefore not work on x86_64.

You may want to install [F-Droid](https://f-droid.org/) to get applications graphically. Note that the Google Play Store will not work as is, because it relies on the proprietary Google Play Services, which are not installed.

___
## Waydroid Prop Options
___
Waydroid uses various properties in order to tell the underlying Android system how to behave in a few places. To do this, we use the `waydroid prop` command. To unset a prop, `waydroid prop set <property> ""`

### Properties

- waydroid prop set persist.waydroid.multi_windows true/false (bool) Enables/Disables persistent freeform window mode
- waydroid prop set persist.waydroid.invert_colors true/false (bool) Swaps the color space from RGBA to BGRA (only works with our patched mutter so far)
- waydroid prop set persist.waydroid.height_padding 0-9999 (int) Adjust Height padding (30 will allow you to use navbar on mobile)
- waydroid prop set persist.waydroid.width_padding 0-9999 (int) Adjust width padding
- waydroid prop set waydroid.display_width 0-9999 (int) (auto-generated) Auto generated size of Waydroid screen
- waydroid prop set persist.waydroid.width 0-9999 (int) Used for user to override desired resolution
- waydroid prop set persist.waydroid.suspend true/false (bool) Keep Waydroid awake and do not let container sleep

___
## Setting up a shared folder
___

Setting up a shared folders to copy files from `source` to `target`.   

!!!dark
`Source` files will be accessible from `Target` but not Editable.
!!!

```sh
sudo mount --bind <source> <target>
```

!!!dark
We will setup the `host` folder to copy files from the host, and the `droid` folder to copy files from waydroid.
!!! 

Example:

- Copy files from Linux to Waydroid: 
    - on Waydroid Create a `/Waydroid/host` folder
    - on Host Create a `~/Waydroid/host` folder
```sh
mkdir ~/Waydroid/host
```
    - Bind Linux folder to the Android one
```sh
sudo mount --bind ~/Waydroid/host ~/.local/share/waydroid/data/media/0/Waydroid/host
```

- Copy files from Waydroid to Linux : 
    - on Waydroid Create a `/Waydroid/droid` folder
    - on Host Create a `~/Waydroid/droid` folder
```sh
mkdir ~/Waydroid/droid
```
    - Bind Linux folder to the Android one
```sh
sudo mount --bind ~/.local/share/waydroid/data/media/0/Waydroid/droid ~/Waydroid/droid
```

___
## Clipboard
___

!!!dark
Replace `dnf` with the appropriate command for your distro.
!!!

[!badge variant="light" text="Step 1"] Install pip

```sh
sudo dnf install pip
```

[!badge variant="light" text="Step 2"] install wl-clipboard

```sh
sudo dnf install wl-clipboard
```

[!badge variant="light" text="Step 3"] install pyclip

```sh
pip install --upgrade pip pyclip
```

[!badge variant="light" text="Step 4"] add `$HOME/.local/bin/` to your $PATH

add

```
export PATH="$PATH:$(du "$HOME/.local/bin/" | cut -f2 | tr '\n' ':' | sed 's/:*$//')"
```

to the appropriate file `.zshenv` or `.bashrc` or `.profile`

[!badge variant="light" text="Step 5"] reboot the system

