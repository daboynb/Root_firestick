# root_firestick
This guide is written for a deice that has note yet been set up.

As the devs say: " This is for the 3rd gen Fire TV Stick (sheldonp) and Fire TV Stick Lite (sheldon)."

# All the credit goes to the devs. This is only a guide, because I've spent a lot of time fixing all the issues and I hope that someone will find this useful.

Devs thread links:
-  https://forum.xda-developers.com/t/unlock-root-twrp-unbrick-fire-tv-stick-3-and-fire-tv-stick-lite-sheldon-p.4410297/ (exploit and twrp)
-  https://github.com/0815hoffi/FireTV-Root-Settings/releases/tag/Latest (settings menu)
-  https://github.com/topjohnwu/Magisk (magisk)

The kamakiri.zip from xda fails, this one instead has been fixed by commenting those lines (thanks to nicedog user on xda):

 - if rpmb != b"\x00" * 0x100:
 - dev.reboot()
 - raise RuntimeError("downgrade failure, giving up")

# Flash twrp


1) Download the kamakiri.zip an unzip it
2) Pre-steps:
    - "sudo apt install python3 python3-serial python3-usb adb fastboot dos2unix"
    - "sudo systemctl stop ModemManager"
    - "sudo systemctl disable ModemManager"
3) On terminal type "sudo ./bootrom-step.sh"
4) Using a cable, connect the stick to the pc
5) After the script finishes and the stick is on fastoot mode, run "./fastboot-step.sh"
6) Now, after the script has succeded, the twrp will appear but you will be unable to use it since it will ask to swipe to allow modifications
7) Now that the recovery is installed type "adb reboot"


# Setup


8) When it boots, it will ask for a network to connect. Now we have two solutions:
    - [The one I used] If you have a rooted phone install adaway, and block into the host file these domains (amzdigitaldownloads.edgesuite.net - softwareupdates.amazon.com - updates.amazon.com). Now enable tethering and use that connection. Go to point 9.
    - Set up the connection and turn off the router while it is searching for updates (a little risky if it you are not fast enough)
9) Now a screen will appear, which will say "Unable to check for updates, retry or reboot the stick"
10) Press and hold the BACK and MENU buttons simultaneously on the remote for a few seconds, until the VoiceView accessibility feature turns on. Then, once the VoiceView feature is on the screen, press the BACK button on the remote to exit VoiceView.
11) Now it will ask for an account, log-in as fast as you can and disable internet if you have not followed the adaway method! Go to #Extras before enabling it.


# Rooting


12) Enable adb, put magisk.zip on the /storage/emulated/0 and type "adb reboot recovery" 
13) When you are into the twrp type:
    - "adb shell twrp install /storage/emulated/0/magisk.zip" 
    or if not work
    - "adb shell twrp install path_of_magisk_from_the_pc"
14) When The install will finish, reboot with "adb reboot"
15) Boot the firestick and now you are rooted!


# Custom launcher, because the stock one is full of ads!

16) Download wolf launcher (or what you want)
17) With adb, type: "adb install com.markus.firetools.apk" and "adb install wolf_launcher.apk"
18) Open the launcher 
19) On adb type su and accept magisk prompt 
20) With adb, type: "adb shell pm disable-user com.amazon.firehomestarter" and "adb shell pm disable-user com.amazon.tv.launcher"
21) Now the firestick will ask to choose wich launcher you want. Choose it and enjoy! Now pressing the home button will bring you back to the custom launcher
22) Disabling the stock launcher will cause you to lose the settings control. This is why we have installed markus.firetools. On wolf launcher tapping on firetv settings will open the firetools that lets you access the settings without any problems!


# Extras


23) To enable the mouse, type "adb install mouse_toggle.apk", for those programs, like adway, which are not designed for use on the TV, where you are unable to use with the remote as a cursor. If it's blocked on startup, disable and then re-enable adb and unknown sources.
24) To disable ota:
    - adb shell pm disable-user --user 0 com.amazon.device.software.ota.override
    - adb shell pm disable-user --user 0 com.amazon.device.software.ota
