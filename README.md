# root_firestick
This guide is written starting with a device out of the box not set up.

As the dev say " This is for the 3rd gen Fire TV Stick (sheldonp) and Fire TV Stick Lite (sheldon)."
All the credits goes to the devs, this is only a guide because I've spent a lot of time fixing all the issues and I hope that someone will find this useful.

Devs thread links:
-  https://forum.xda-developers.com/t/unlock-root-twrp-unbrick-fire-tv-stick-3-and-fire-tv-stick-lite-sheldon-p.4410297/ (exploit and twrp)
-  https://github.com/0815hoffi/FireTV-Root-Settings/releases/tag/Latest (settings menu)
-  https://github.com/topjohnwu/Magisk (magisk)


# Flash twrp


1) Download the kamakiri.zip an unzip it
2) Pre-steps:
    - "sudo apt install python3 python3-serial python3-usb adb fastboot dos2unix"
    - "sudo systemctl stop ModemManager"
    - "sudo systemctl disable ModemManager"
3) On terminal type "sudo ./bootrom-step.sh"
4) Connect the stick with a cable to the pc
5) After the script finish and the stick is on fastoot mode run "./fastboot-step.sh"
6) Now after the script succeded the twrp will appear but you will be unable to use it since it will ask to swipe to allow modifications
7) Now that the recovery is installed type "adb reboot"


# Setup


8) When it will boot it will ask for a network to connect, now we have two solutions:
    - [The one I used] Having a rooted phone install adaway, and block into the host file those domains (amzdigitaldownloads.edgesuite.net - softwareupdates.amazon.com - updates.amazon.com). Now enable tethering and use that connection. Goto point 9.
    - Setting up the connection and turn of the router while is searching for updates (a little risky if it you are not fast enough)
9) Now will appear a screen that will say "Unable to check for updates, retry or reboot the stick"
10) Press and hold the BACK and MENU buttons simultaniously on the remote for a few seconds until the VoiceView accessibility feature turns on, then once the VoiceView feature is on the screen, press the BACK button on the remote to exit VoiceView.
11) Now it will ask for an account, log-in fastest as you can and disable internet if you have not followed the adaway method! Goto #Extras before enable it.


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
17) With adb type "adb install com.markus.firetools.apk" and "adb install wolf_launcher.apk"
18) Open the launcher 
19) On adb type su and accept the prompt of magisk 
20) With adb type "adb shell pm disable-user com.amazon.firehomestarter" and "adb shell pm disable-user com.amazon.tv.launcher"
21) Now the firestick will ask to choose wich launcher you want, choose it and enjoy! Now pressing the home button will bring back to the custom launcher
22) Disabling the stock launcher you will lose the settings control, this is why we have installed markus.firetools. On wolf launcher tapping on firetv settings will open the firetools that lets you access to the settings without any problems!


# Extras


23) Mouse enabler "adb install mouse_toggle.apk" for those programs that are not designed for TV, like adway where you are unable to use with the remote without a cursor (If it's blocked on starting, enable and disable adb and unknow sources)
24) Disable ota:
    - adb shell pm disable-user --user 0 com.amazon.device.software.ota.override
    - adb shell pm disable-user --user 0 com.amazon.device.software.ota
