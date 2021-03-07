# Hackintosh-BigSur-X510UR-BQ166T
My files and info of a Big Sur Hackintosh build on a ASUS X510UR-BQ166T

[macOS BigSur config screenshot](/Screenshots/BigSur-Config.png?raw=true)

First thing you need to know is that you probably will encounter problems, even if your rig is the same as mine. If you don't know what you are doing don't even get started or you will get frustated. Hackintosh isn't as simple as a step by step guide. Read everything before you start.
Don't do it if you depend on this laptop for deadlines, this may take time until you suceed.

This is a work in progress documentation, that only shows what worked for me. I'm not a hackintosh expert. Feel free to ask questions or share experience about this hardware and some related ones (VivoBook X510* mostly).

## Bootloader

I'm using OpenCore 0.6.7 as bootloader. I did a fresh install following the [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/). To boot **Big Sur Installer** from a USB Drive you will need to make the bootable drive from another macOS(What I did was previously install macOS Catalina with Clover and then built the bootable drive from it). It's worth to mention that in my EFI folder and config.plist I'm not using debug files nor configs, but I recommend you do until you get everthing going. After that you can choose keep debuging for eventual panic errors or disable it. I added OpenCanopy.efi and enabled OpenCore GUI for boot, thats only cosmetic but I don't know if can cause problems when booting for installer or with debugging. Check Post Install section for disabling it if using my config.plist.

## Status of the system

### :heavy_check_mark: Networking
Using [itlwm](https://openintelwireless.github.io/itlwm/) to enable the Intel Wifi card (Intel(R) Dual Band Wireless AC 8275) as this doesn't require me to switch my Wifi Card for a natively compatible. 

#### Relevant Kexts
- AirportItlwm.kext

### :heavy_check_mark: Graphics
Only intel integrated HD620 shared memory graphics are available. The 930MX is explicitly deactivated.
Here my build differs from @luisdecker from which I forked the project. My CPU isn't the same from his and what I did is to reconfigure framebuffers to HD620 indicated ones in WhateverGreen Manual. 

#### Relevant Kexts:
- WhateverGreen.kext

### :heavy_check_mark: Pointing device and keyboard
You may need a usb mouse to install the hack, as touchpad may wont work until later on.
For me touchpad worked since macOS Installer.

#### Relevant Kexts:
- VoodooI2C.kext
- VoodooI2CHID.kext
- VoodooPS2Controller.kext

### :heavy_check_mark: Bluetooth
Working normally.
Had some problems with my G603 Mouse but from what I could find is a long date problem with macOS for this specific mouse, works fine with dongle though.

#### Relevant Kexts
- IntelBluetoothInjector.kext
- IntelBluetoothFirmware.kext

### :heavy_check_mark: Battery Measurement
Working normally.

#### Relevant Kexts
- SMCBatteryManager.kext

#### Relevant DSDT's
- SSDT-BATT.aml

### :heavy_check_mark: Sound 
:heavy_check_mark: Internal speakers 
 
:heavy_check_mark: Internal Microphone 

:heavy_check_mark: Headphones 

:heavy_check_mark: Bluetooth earphones 

#### Relavant Kexts
- AppleALC.kext

### CPU power scheduling
~~I tuned CPUFriend (Using CPUFriendFriend) to a more performance-oriented frequecy scheduler.~~
Here I tuned my build to a balanced-power frequency scheduler using CPUFriendFriend aswell. And made sure LFM was set right for my CPU or macOS will have trouble waking up from sleep.

#### Relevant Kexts
- CPUFriend.kext

### :heavy_check_mark: Sleep
Appears to be working fine, just did some of the recommendations from Dortania's Guide for Sleep Fix. Not explict saying what I did because you will need debuging and checking from guide for specific clues.
**Not heavily tested.** 

# EFI
The EFI folder attached is the one I'm using currently. The kexts attached are the ones recommended by OpenCore Install Guide, and the ones listed above. Fixes intel graphics, touchpad, battery indicator, audio, bluetooth and Wifi. 

# Guide

Follow the [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/). Some DSDT's, kexts and configurations here presented may be used before the install to fix some of the issues mentioned above.
