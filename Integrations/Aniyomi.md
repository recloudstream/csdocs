---
label: Aniyomi
order: 994
icon: /static/aniyomi.png
---

### Use your Aniyomi Extensions in CloudStream!
Not guaranteed to work perfectly. Please make an issue if any functional extension does not work with this system.

Add this repository using this shortcode: [anicompat](https://raw.githubusercontent.com/CranberrySoup/AniyomiCompatExtension/master/repo.json)

~~Click~~ Pet the gorilla to install it on your phone:

[![gorilla](https://cdn.jsdelivr.net/gh/twitter/twemoji@latest/assets/72x72/1f98d.png)](cloudstreamrepo://raw.githubusercontent.com/CranberrySoup/AniyomiCompatExtension/master/repo.json)

### Installation

Install the extension in CloudStream. The extension should then download the internal compat APK automatically. Once the installation is complete your Aniyomi extensions should appear in CloudStream.

Installing this plugin does __not__ automatically download all Aniyomi extensions, you still need to get those from Aniyomi.

### Aniyomi extension list

You can find the list of all Aniyomi extensions [here](https://aniyomi.org/extensions/).

---

### Troubleshooting

**No Aniyomi extensions appear**

1. Go to plugin settings _(Settings -> Extensions -> Aniyomi Compat -> Click the extension settings button next to the trashcan)_
2. Check that the compat apk is installed correctly by checking what it says under the **Currently Using:** tab. It should show some long path to an APK file. If it says none click **Force download APK**.
3. If step 2 does not work, grab the APK and install it yourself [here](https://github.com/CranberrySoup/AniyomiCompat/raw/builds/app-debug.apk)
4. Make sure that you actually have Aniyomi Extensions installed. It should show something other than 0 after **Number of extensions**

**Aniyomi extensions do not work**

1. Make sure the extension is functioning in Aniyomi.
2. Try downloading the compat APK instead of using it internally. Download [here](https://github.com/CranberrySoup/AniyomiCompat/raw/builds/app-debug.apk) or click Install APK externally in plugin settings.
3. Restart CloudStream
4. Make an issue here if it still does not work
