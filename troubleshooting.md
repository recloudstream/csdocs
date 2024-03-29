---
label: Troubleshooting
order: 700
icon: tools
---

## Basic

==- Repositories/Extensions are not loading.
If the repositories are not loading in [the official site](https://recloudstream.github.io/public-gateway-checker/) or in the [!badge variant="dark" text="Extensions"] section, repeat the process using VPN connection.
===

==- `XYZ` extension is not loading.
1. Open the site in  the browser. If the site is not loading in browser also, use VPN or try [!badge variant="dark" text="site cloning"](/Settings/cloningsite.md).
2. If the site is working in browser, post a report in the `reports` channel.
===

==- Backup error
Change/reselect the download location.
[!badge variant="dark" icon="/static/base.png" text="Cloudstream"] → [!badge variant="dark" icon="/static/gear.png" text="Settings"] → [!badge variant="dark" icon="download" text="download path"] and then select a custom location.
===

==- Restore backup error
Rename the extension of the file from `json to txt`. Now try again to read the backup file.
===

==- Error: Out of memory
Change the video cache on disk. [!badge variant="dark" icon="/static/base.png" text="Cloudstream"] → [!badge variant="dark" icon="/static/gear.png" text="Settings"] → [!badge variant="dark" text="player"] > [!badge variant="dark" icon="server" text="video cache on disk"] and set a **lower amount of cache**.
===

==- Safe mode on
Clear the app cache and restart the app. You can also set a lower amount cache to avoid this issue.
!!!contrast This is a general troubleshooting. May not fix the issue. Then post it in the reports channel.
!!!
===

## Subtitles
==- Broken Subtitles
[!badge variant="dark" text="Video player"] → [!badge variant="dark" text="sources"] → [!badge variant="dark" text="subtitles"] and click the [!badge variant="dark" text="Auto"] at the top. Now change the encode of the subtitle language.

![](https://media.discordapp.net/attachments/1015131233824538624/1072223726130692216/VIu1MFB.png)

![](https://media.discordapp.net/attachments/1015131233824538624/1072224426084532225/iKMhqlW.png)
===

==- Subtitles casting issue
If subtitle isn't casting on the tv with the native casting system., try casting using [this app](https://play.google.com/store/apps/details?id=com.instantbits.cast.webvideo).

[!badge variant="dark" icon="/static/base.png" text="Cloudstream"] → [!badge variant="dark" text="Episode page"] → **Press and hold the epsiode** → [!badge variant="dark" text="play with Web Video Cast"] → **choose the link and then cast.** *The subtitle selection maybe not as good as cs3.*
===

## Sorastream

==- The episode loading is taking too long.
As it scrapes a lot of sites, it takes time to load all of them. Skip loading after 3-5 seconds.
===

==- Some sources are not loading.
1. Sora has some geo restricted sources. Use a VPN to access those sources.
2. Or, exo player can't handle the video. Use external player like VLC.
===


==- Some titles are showing "No links found".
Sora uses TMDb for catalogue, not the sources. So, it may show titles that no site has.
===

==- Some videos are not playing video/audio.
EXO player can't handle the video. Use external player like VLC.
===

==- Video Download error.
Try 1DM to download from Sorastream
===

## WSA

==- Install.ps1 is not recognized/missing

![](https://media.discordapp.net/attachments/1044322950725259274/1068243571544690719/9Qf3veK.png)

 If the popup windows disappear without asking administrative permission and Windows Subsystem For Android™ is not installed successfully, you should manually run Install.ps1 as administrator:
      
1. Press Win+x and select Windows™ Terminal (Admin)
      
2. Input the command below and press enter, replacing {X:\path\to\your\extracted\folder} including the {} with the path of the extracted folder
    ```Powershell
        cd "{X:\path\to\your\extracted\folder}"
     ```  
        
3. Input the command below and press enter   
    ```Powershell
        PowerShell.exe -ExecutionPolicy Bypass -File .\Install.ps1
    ```
        
4. The script will run and Windows Subsystem For Android™ will be installed
===

==- Virtualization Error

![](https://user-images.githubusercontent.com/68629435/213985345-a6fc6e97-63f3-4741-8965-8d62a0d6b824.png)

1. Remove WSA

2. Go to "Turn Windows features on and off" and disable Hyper-V, Virtual Machine Platform, Windows Hypervisor Platform, and Windows Subsystem for Linux, then restart.

3. Reenable these features and restart a second time.

4. Make sure Core Isolation is turned off.

5.  In registry editor (regedit), go to `\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\FsDepends`

    Change the value of “Start” from `3` to `0`

!!!
You can change it back to 3, if it makes no difference
!!!

6. Then in CMD (Run as Adminstrator), paste:
```cmd
bcdedit /set hypervisorlaunchtype auto
```
7. Reinstall WSA by running `Run.bat`
===

