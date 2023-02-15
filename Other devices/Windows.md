---
label: Windows
order: 999
icon: /static/win11.png
---

# WSA Installation Guide

==- MagiskonWSA (Windows 10 & 11)

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
| **Partition**: NTFS <br /> Windows Subsystem For Android™ can only be installed on a NTFS partition, not on an exFAT partition | **Partition**: NTFS <br /> Windows Subsystem For Android™ can only be installed on a NTFS partition, not on an exFAT partition|
| The Computer must support virtualization and be enabled in BIOS/UEFI and Optional Features. [**Guide for this process.**](https://support.microsoft.com/en-us/windows/enable-virtualization-on-windows-11-pcs-c5578302-6e43-4b4b-a449-8ced115f58e1)| The Computer must support virtualization and be enabled in BIOS/UEFI and Optional Features. [**Guide for this process.**](https://support.microsoft.com/en-us/windows/enable-virtualization-on-windows-11-pcs-c5578302-6e43-4b4b-a449-8ced115f58e1)|

!!!warning GPU compatibility
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

!!!dark
If you previously have a MagiskOnWSA installation, it will automatically uninstall the previous one while preserving all user data and install the new one, so don't worry about your data.
!!!


[!badge variant="light" text="Step 4"] Once the installation process completes, WSA will launch.

!!!dark
If this is a first-time install, a window asking for consent to diagnostic information will be shown. Sometimes two identical windows may appear, click OK in both windows).
!!!

!!!light The installation Process is DONE!
Now close Windows powershell by putting any key there.
!!!

!!!contrast Troubleshooting
If you face any issue installing WSA, join the [**Support Server**](https://discord.com/invite/2thee7zzHZ). The common fixes are listed [!badge text="here"](/troubleshooting.md/#wsa). You can follow these too.
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

1. [Download the latest build](https://github.com/MustardChef/WSABuilds#downloads) (that you want to update to)
2. Make sure Windows Subsystem For Android is not running (Click on "Turn off" in the WSA Settings and wait for the spinning loader to disappear)
2. Using 7-Zip, WinRAR or any other tool of choice, open the .zip file 
3. Within the .zip archive open the subfolder (Example: WSA_2xxx.xxxxx.xx.x_xx_Release-Nightly-with-magisk-xxxxxxx-MindTheGapps-xx.x-RemovedAmazon)
4. Select all the files that are within this subfolder and extract them to the current folder where the file for Windows Subsystem For Android are (the folder you extracted, and installed WSA from)
5. When prompted to replace folders, select "Do this for all current items" and click on "Yes" 
6. When prompted to replace files, click on "Replace the files in the destination"
7. Run  the ``Run.bat`` file
8. Launch Windows Subsystem For Android Settings app and go to the ``About`` tab using the sidebar
9. Check if the WSA version matches the latest version/ the version number that you want to update to

___
## Backup & Restore

### Backup
If you want to preserve your data, make a backup of the file `%LOCALAPPDATA%\Packages\MicrosoftCorporationII.WindowsSubsystemForAndroid_8wekyb3d8bbwe\LocalCache\userdata.vhdx`.

### Restore
Paste the VHDX file back to the folder `%LOCALAPPDATA%\Packages\MicrosoftCorporationII.WindowsSubsystemForAndroid_8wekyb3d8bbwe\LocalCache` .

___
## Uninstallation

1. Make sure that Windows Subsystem For Android™ is not running
2. Search for ``Windows Subsystem For Android™ Settings`` using the built-in Windows Search, or through Add and Remove Programs and press uninstall
3. Delete the WSA folder that extracted you extracted and Run.bat was run from to install WSA (MagiskOnWSA folder)
4. Go to ``%LOCALAPPDATA%/Packages/`` and delete the folder named ``MicrosoftCorporationII.WindowsSubsystemForAndroid_8wekyb3d8bbwe``
  - If you get an error that states that the file(s) could not be deleted, make sure that WSA is turned off

===

==- WSA (Windows 11 only)

!!!info This WSA build includes
- Non-rooted Android 13 (You can't access Android folder)
- No Google Play Services and Magisk
- Amazon Appstore
!!!
___
## Installation

Download and Install Windows Subsystem for Android from the [**Store**](https://apps.microsoft.com/store/detail/windows-subsystem-for-android%E2%84%A2-with-amazon-appstore/9P3395VX91NR?hl=en-us&gl=us).

!!!light Changing region
If your region doesn't have WSA in the microsoft store, you can change the region to get it.
1. Select [!badge variant="dark" text="Start"] → [!badge variant="dark" text="Settings"] → [!badge variant="dark" text="Time & Language"] → [!badge variant="dark" text="Language & Region"].
2. Under [!badge variant="dark" text="Country or region"], select your new region. (Recommendation: US)
3. You can switch back to your original region at any time.
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

[!embed](https://www.youtube-nocookie.com/embed/m4JA-4tWM_o)

!!!dark More stuff
If you want more installation method, read [this article](https://www.androidpolice.com/set-up-wsa-windows-11-android-apps/).
!!!

===
