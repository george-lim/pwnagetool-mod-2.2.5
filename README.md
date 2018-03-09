PwnageTool Mod 2.2.5
<br>
![GitHub downloads](https://img.shields.io/github/downloads/george-lim/pwnagetool-mod-2.2.5/total.svg)
[![GitHub release](https://img.shields.io/github/release/george-lim/pwnagetool-mod-2.2.5.svg)](https://github.com/george-lim/pwnagetool-mod-2.2.5/releases)
[![GitHub issues](https://img.shields.io/github/issues/george-lim/pwnagetool-mod-2.2.5.svg)](https://github.com/george-lim/pwnagetool-mod-2.2.5/issues)
[![GitHub pull requests](https://img.shields.io/github/issues-pr/george-lim/pwnagetool-mod-2.2.5.svg)](https://github.com/george-lim/pwnagetool-mod-2.2.5/pulls)
[![license](https://img.shields.io/github/license/george-lim/pwnagetool-mod-2.2.5.svg)](https://github.com/george-lim/pwnagetool-mod-2.2.5/blob/master/LICENSE)
===============

This repo contains all of my research and progress trying to get the latest version of Cydia running on iPhone OS 2.0. To read more about PwnageTool, click [here](https://www.theiphonewiki.com/wiki/PwnageTool).

1. [The Current State](#the-current-state)
1. [My Custom Firmware](#my-custom-firmware)
1. [DIY Custom Firmware](#diy-custom-firmware)
1. [The Process](#the-process)

# The Current State
Long story short, I modified the iPhone Dev Team's `PwnageTool v2.2.5` to accept the following bundles,

```
iPhone1,1_2.0_5A347.bundle
iPhone1,2_2.0_5A347.bundle
iPod1,1_2.0_5A347.bundle
```

and replaced the default `CydiaInstaller.bundle` with an updated bundle from `PwnageTool v5.1.1`, effectively installing Cydia 1.1.x on the custom firmware and thereby fixing the unsupported Cydia error.

I also removed `Installer.bundle` because Installer no longer works.

This mod also restores the feature of downloading Cydia packages back to PwnageTool, so if you need to download any Cydia packages, you may do so without fail. Just make sure to install all dependencies for your package as well.

**However**, Cydia itself does have one quirk that I cannot seem to solve. When Cydia is launched, it always returns an `Unable to Load (untrusted server certificate)` error. There is no crashing, and Cydia successfully updates its sources but I cannot install / view any new packages within the app. A quick Google search will tell you that you need to manually update the date / time settings on your iPhone to fix the issue, but this didn't work on my iPhone 3G. I suspect that Cydia doesn't issue trusted certificates on iPhone OS 2.0 devices running Cydia 1.1.x. **Please let me know if you managed to fix this error.**

To work around the issue, you can install OpenSSH and use `Cydia AutoInstall` to install packages manually by SSH-ing the packages over.

# My Custom Firmware
[Here](https://github.com/george-lim/pwnagetool-mod-2.2.5/releases/download/v1.0/iPhone1.2_2.0_5A347_Custom_Restore.ipsw) is the download to my custom iPhone OS 2.0 firmware for iPhone 3G. It should be sufficient for anyone who just wants to get iPhone OS 2.0 on their phone ASAP. It has the latest version of OpenSSH installed (as of March 2018) which fully works. To install, you'll need to put your iPhone 3G in Pwned DFU mode and do an iTunes restore.

```
iPhone1,2_2.0_5A347_Custom_Restore.ipsw
MD5: 86a291eb9fb49f2432ef056b1a0e3348
SHA1: 3673779a498a995847ae6c35271568f0bcce70ba
```

The firmware has the following modified properties:
```
Hacktivated: YES
Root Partition Size: 1000 MB (double default size)
Custom Boot Logo / Recovery Image: NONE
```

**SIDE NOTE:** I cannot seem to install the latest version of Cydia from PwnageTool on the custom firmware without Cydia crashing, so I have updated every default package on the iPhone except for packages tied to `Cydia Installer`.

Updated default packages include:
```
Bourne-Again SHell
bzip2
Core Utilities (/bin)
Cydia Translations
Darwin Tools
Debian Utilities
Find Utilities
gzip
LZMA Utils
New Curses
PAM (Apple)
PAM Modules
pcre
readline
sed
shell-cmds
system-cmds
Tape Archive
UIKit Tools
```

Default packages that could not be updated include:
```
APT 0.7 Strict (lib)
Cydia Installer
Debian Packager
```

Extra installed packages include:
```
OpenSSL
OpenSSH
```

# DIY Custom Firmware
Of course, if you want to customize your own firmware or add your own packages, you may do so with the provided PwnageTool app. Nothing in the UI has changed so you should create your firmware as you would normally.

```
PwnageTool_2.2.5.dmg
MD5: 77330df69ec86498071c4c5025b1b1a9
SHA1: 81c15d7f23edb860e3b10c5052e469347deee194
```

# The Process
This is likely the furthest I will go with this project. Everything started when I was cleaning out my closet a few days back, when I found an Apple 30-pin to USB cable lying beside my old iPhone 3G. I decided to downgrade my iPhone 3G to iPhone OS 2.0 and re-jailbreak it to satisfy my nostalgia.

I feel like I have tried everything to get Cydia to run properly on iPhone OS 2.0. I've done countless testing with various versions of `WinPwn` and `QuickPwn`, all without success. None of them install a version of Cydia that wants to update to the latest version. I decided to settle on using PwnageTool because I read [this article](http://www.iclarified.com/13009/how-to-add-a-firmware-bundle-to-pwnagetool) which showed how to add non-native firmware support to PwnageTool. From this, I found out that I could also manually update the `CydiaInstaller.bundle` in PwnageTool to "update" Cydia.

If you want to play around with, or modify a version of PwnageTool, here are the steps I did to modify PwnageTool.

Firstly, go to [axi0mX's PwnageTool-mirror repo](https://github.com/axi0mX/PwnageTool-mirror) and download `PwnageTool_2.0.2.tbz` and `PwnageTool_2.2.5.dmg`. Go to [iDownloadBlog's download page](http://www.idownloadblog.com/download/) and download the latest version of PwnageTool (file should be called `PwnageTool_5.1.1.dmg`). Put these files in a new project folder.

Run and copy `PwnageTool.app` from `PwnageTool_2.2.5.dmg` into your project folder. Rename this file to `PwnageTool-2.2.5.app`.

Extract `PwnageTool.app` from `PwnageTool_2.0.2.tbz`. Rename this file to `PwnageTool-2.0.2.app`. Right click the app, `Show Package Contents` and navigate to `Contents/Resources/FirmwareBundles` and copy all of the 2.0 bundle files to your project folder. You're now done with `PwnageTool_2.0.2.tbz` as well as `PwnageTool-2.0.2.app`. Feel free to delete them.

Run and copy `PwnageTool.app` from `PwnageTool_5.1.1.dmg` into your project folder. Rename this file to `PwnageTool-5.1.1.app`. Right click the app, `Show Package Contents`, navigate to `Contents/Resources/CustomPackages`, and copy `CydiaInstaller.bundle` to your project folder. Navigate to the copied bundle, right click, `Show Package Contents` and edit `Info.plist` using any text editor.

Replace the `SupportedFirmware` key and array with the following code.
```
<key>SupportedFirmware</key>
<array>
    <string>iPhone1,1_2.0_5A347</string>
    <string>iPhone1,2_2.0_5A347</string>
    <string>iPod1,1_2.0_5A347</string>
    <string>iPhone1,1_2.0.1_5B108</string>
    <string>iPhone1,2_2.0.1_5B108</string>
    <string>iPod1,1_2.0.1_5B108</string>
    <string>iPhone1,1_2.0.2_5C1</string>
    <string>iPhone1,2_2.0.2_5C1</string>
    <string>iPod1,1_2.0.2_5C1</string>
    <string>iPhone1,1_2.1_5F136</string>
    <string>iPhone1,2_2.1_5F136</string>
    <string>iPod1,1_2.1_5F137</string>
    <string>iPhone1,1_2.2_5G77</string>
    <string>iPhone1,2_2.2_5G77</string>
    <string>iPod1,1_2.2_5G77</string>
    <string>iPhone1,1_2.2.1_5H11</string>
    <string>iPhone1,2_2.2.1_5H11</string>
    <string>iPod1,1_2.2.1_5H11</string>
</array>
```

You're now done with `PwnageTool_5.1.1.dmg` as well as `PwnageTool-5.1.1.app`. Feel free to delete them.

Now, open another Finder window and navigate inside the `PwnageTool-2.2.5.app` by showing package contents. Replace the existing `CydiaInstaller.bundle` in the CustomPackages folder with your updated version. Add the three firmware bundles from earlier to the FirmwareBundles directory and you're done. You should now run `PwnageTool-2.2.5.app` to see the results!
