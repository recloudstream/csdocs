---
label: Windows
order: 999
icon: /static/win11.png
---

# WSA Installation Guide

!!!info This WSA build includes
- Rooted Android 13
- Google Play Services and Magisk
- No Amazon App store
!!!

## Requirements
___
|     [!badge variant="primary" size="l" icon="/static/win11.svg" text="Windows 11"]    |    [!badge variant="primary" size="l" icon="/static/win10.svg" text="Windows 10"]  { class="compact" }     |
|:-------------------------:|:-----------------------:|
| **RAM**: 6 GB (minimum) and 16 GB (recommended).| **RAM**: 6 GB (minimum) and 16 GB (recommended).|
| **Build**: 22000.526 or higher.| **Build**: 22H2 10.0.19045.2311 or higher.|
| - Partition: NTFS <br /> Windows Subsystem For Android™ can only be installed on a NTFS partition, not on an exFAT partition |- Partition: NTFS <br /> Windows Subsystem For Android™ can only be installed on a NTFS partition, not on an exFAT partition|
| The Computer must support virtualization and be enabled in BIOS/UEFI and Optional Features. [**Guide for this process.**](https://support.microsoft.com/en-us/windows/enable-virtualization-on-windows-11-pcs-c5578302-6e43-4b4b-a449-8ced115f58e1)| The Computer must support virtualization and be enabled in BIOS/UEFI and Optional Features. [**Guide for this process.**](https://support.microsoft.com/en-us/windows/enable-virtualization-on-windows-11-pcs-c5578302-6e43-4b4b-a449-8ced115f58e1)|

!!!warning GPU
Any compatible Intel, AMD or Nvidia GPU. GPU Performance may vary depending on its compatibility with Windows Subsystem For Android™. Nvidia GPUs are known to cause problems. If Windows Subsystem For Android™ does not start or there are graphical glitches when an Nvidia GPU is used, [follow this guide](https://github.com/MustardChef/WSABuilds/blob/master/Guides/ChangingGPU.md) to switch to another iGPU/dGPU/eGPU  that you may have or Microsoft Basic Renderer.
!!!

___
## Installation

!!!warning If you have the official WSA installed, you must [completely uninstall](#uninstallation) it to use MagiskOnWSA.
!!!

[!badge variant="light" text="Step 1"] **Download the WSA** zip file from [!badge variant="secondary" text="here"](https://github.com/MustardChef/WSABuilds#downloads)

!!!danger Do not download "Source code".
!!!

[!badge variant="light" text="Step 2"] **Extract** the zip file

[!badge variant="light" text="Step 3"] Open the WSA folder and **run** the `Run.bat`

[!badge variant="light" text="Step 4"] Once the installation process completes, WSA will launch.

!!!info If this is a first-time install, a window asking for consent to diagnostic information will be shown. Sometimes two identical windows may appear, click OK in both windows).
!!!

!!!info The installation Process is DONE!
Now close Windows powershell by putting any key there.
!!!

___
## Sideloading

[!badge variant="light" text="Step 1"] Download and install [**WSA Pacman**](https://github.com/alesimula/wsa_pacman/releases) or [**WSA Sideloader**](https://github.com/infinitepower18/WSA-Sideloader).

[!badge variant="light" text="Step 2"] Go to [!badge variant="dark" text="Windows Subsystem for Android"] → [!badge variant="dark" text="Developer"] and turn on **Developer mode**.

!!!danger You have to give pacman or other sideloaders the adb permission.
![](https://media.discordapp.net/attachments/1015131233824538624/1062611905249820733/allow.png)
!!!

!!!info If the "Install" button is greyed out while installing apk
**Open** WSA pacman and **turn on** wsa from there.
![](https://media.discordapp.net/attachments/1015131233824538624/1062610433506287708/WSA-pacman_x7UaiviLSW.png)
!!!

___
## Update

**Merge** the new and the old wsa folder and **replace** the old files with the new ones.

___
## Backup & Restore

### Backup
If you want to preserve your data, make a backup of the file `%LOCALAPPDATA%\Packages\MicrosoftCorporationII.WindowsSubsystemForAndroid_8wekyb3d8bbwe\LocalCache\userdata.vhdx`.

### Restore
Paste the VHDX file back to the folder `%LOCALAPPDATA%\Packages\MicrosoftCorporationII.WindowsSubsystemForAndroid_8wekyb3d8bbwe\LocalCache` .

___
## Uninstallation

1. Go to the Start Menu
2. Type `Windows Subsystem for Android`
3. Once the WSA app shows, click `App settings` in the right panel.
4. In the Settings window that opens, scroll down and click `Terminate`
5. Click `Repair`
6. Click `Reset`
7. Close the Settings app
8. Go to the Start Menu
9. Type `Windows Subsystem for Android`
10. Once the WSA app shows, click `Uninstall` in the right pane
