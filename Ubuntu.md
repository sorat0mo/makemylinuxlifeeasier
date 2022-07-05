# Installing the system
The [guides](https://itsfoss.com/getting-started-with-ubuntu/) by ItsFoss is amazingly detailed and clear, you should read them. For installation you should read [this](https://itsfoss.com/install-ubuntu-1404-dual-boot-mode-windows-8-81-uefi/). For making a LiveUSB, I recommend using balenaEtcher, I wrote a guide and you can check it out [here](https://loremipsumdotlol.wordpress.com/2022/02/23/create-a-linux-live-usb-with-balena-etcher-and-ventoy/).

# Install other useful tools
These tools will be useful for gaming.

### 1. Feral Gamemode

This will defer system resources to your game, attaining optimal performance when gaming. It is included by default in Ubuntu now. But *not* in Kubuntu, nor is it in KDE Neon.

To install it, do `sudo apt install gamemode`

### 2. Mangohud and GOverlay

Afterburner and Rivatuner is not on Linux, but there is a replacement for the huds. Mangohud replicates that of afterburner and looks pretty good out of the box.

Goverlay is the GUI for configuring mangohud. Keep in mind though, the goverlay version in main Ubuntu repo is **outdated**, so use the author's repo instead:
```
sudo add-apt-repository ppa:flexiondotorg/mangohud
sudo apt-get update
sudo apt-get install goverlay
```
This will install goverlay, mangohud and a few other dependencies.

### 3. Lutris

Lutris is an open source platform for organizing your games. It also makes installing non-Steam, non-Linux games much easier through community installers. I highly recommend using it to simplify installing non-Steam games.

To install:
```
sudo add-apt-repository ppa:lutris-team/lutris
sudo apt update
sudo apt install lutris
```

### 4. Wine and dependencies

This is recommended to maximize wine performance and compatibility. Installing these also allows you to run \*.exe executables and games such as RPGM games not on Steam.

```
wget -nc https://dl.winehq.org/wine-builds/winehq.key
sudo apt-key add winehq.key
sudo apt-add-repository 'https://dl.winehq.org/wine-builds/ubuntu/'
sudo apt update
sudo apt install --install-recommends winehq-staging
sudo apt install winetricks
rm winehq.key
```

### 5. Proton-GE and Wine-GE

These are authored by [@GloriousEggRoll](https://github.com/GloriousEggroll) and come in handy whenever lutris-wine or Steam Proton refuse to work whatsoever.

Refer to the *Native* and *Release Installation* in [GloriousEggroll/proton-ge-custom](https://github.com/GloriousEggroll/proton-ge-custom) and [GloriousEggroll/wine-ge-custom](https://github.com/GloriousEggroll/wine-ge-custom) respectively.

### 6. Nvidia X Server Settings

This is a frustrating piece of crap that I hope I never had to deal with. Whoever wrote this software does not respect user experience and makes it frustrating to use. By frustrating I mean it does not save fan speed controls and powermizer(overclocking) configurations by default.

1. Do the following: `sudo nvidia-settings`, this will open nvidia-settings with root privileges.
2. Configure everything in X Server Display Configuration, and hit **Save to X configuration file**
3. Configure X Screen settings.
4. Configure Fan speed and Powermizer.
5. Make sure you disabled *Include X Display Names in the Config file*
6. Hit *Save Current Configuration* in the tab *nvidia-settings Configuration*
7. Open the saved file and add the following

```
[fan:0]/GPUCurrentFanSpeed=70
[fan:1]/GPUCurrentFanSpeed=70
[gpu:0]/GPUPowerMizerMode=1
```

It detected my card has 2 controllable fans (although it is a 3 fans card), so I put `fan:0` and `fan:1`, if it detects more, just add more. Same with `gpu:0`. PowerMizerMode 1 is "Prefer Maximize Performance".

Save the file and make a startup command like this: `nvidia-settings --load-config-only`. If your distro/flavour does not support startup commands(like Kubuntu), make a bash and just add it as login script.

### 7. PulseEffects

PulseEffects may or may not have bugs depending on your distro, for me, it couldn't properly load and use presets. Rendering my Mono-downmixing settings useless.



**First**, according to [This Post](https://www.linuxuprising.com/2018/05/pulseeffects-nice-system-wide.html), PulseAudio by default may switch to a wrong output device when PulseEffects is enabled, which is undesired. To fix this:



1. Unload the module `module-switch-on-connect` with `pactl unload-module module-switch-on-connect`

2. Write it permanently with:

   ```bash

   cp /etc/pulse/default.pa ~/.config/pulse

   sed -i 's/load-module module-switch-on-connect/#load-module module-switch-on-connect/g' ~/.config/pulse/default.pa

   ```



For KDE, you may also need to unload `module-device-manager`, however, it wasn't loaded for me by default, but give it a try nonetheless:



1. `pactl unload-module module-device-manager`

2. `echo "pactl unload-module module-device-manager > /dev/null 2>&1" >> ~/.bashrc`



The above was supposed to be fixed with newer PulseAudio and PulseEffects versions, but apparently I still had this problem.



**Second**, for some reason PulseEffects refuse to load presets if you start it with just `pulseeffects --gapplication-service` or `pulseeffects --gapplication-service -l abcd`. I tried lots of hacks to fix it, and came across the fix as a simple but effective bash script.


According to one of the replies in [this issues](https://githubmemory.com/repo/wwmm/pulseeffects/issues/952), the following commands are needed:



```bash

#!/bin/bash

(pulseeffects --gapplication-service &)

sleep 1

pulseeffects -l Blankkk

sleep 1

pulseeffects -l OMG

```



Where `Blankkk` denotes a *completely blank* preset and `OMG` denotes your desired preset. Thankfully, the save preset feature still works to an extent.



### 8. XanMod Kernel

The [XanMod Kernel](https://xanmod.org/) is a custom kernel that keeps up-to-date with the latest kernel version and adds its own patch and tweaks for a smoother and faster Linux computing experience. The fact that Ubuntu and its derivatives stay behind with an older kernel (5.13 at the time of writing) forbid using fsync to improve and stabalize in-game performance. The XanMod Kernel is specifically compiled for Debian based distros, and is available for Ubuntu flavours.



To install, following the [Install via Terminal](https://xanmod.org/#install_via_terminal) guide found on XanMod Kernel official website.

To verify you correctly installed the kernel after reboot, issue the command `hostnamectl` in terminal.



