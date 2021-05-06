# EFI for Xiaomi Gaming 7th Generation (KabyLake)

## Disclaimer!
This is a fork from [johnnync13](https://github.com/johnnync13/)https://github.com/johnnync13/XiaomiGaming and I am just porting for the Xiaomi Gaming Book 7th gen with KabyLake. I do not own any copyright.
Use these files and this howto at your own risk. I'm not responsible in any way for lost data, damage to software or hardware or anything else that might go wrong. This works for me but might not for you.

### MacOS Versions tested:
* macOS 10.15 Catalina

### Requirements
* Xiaomi Xiaomi Gaming 7th Generation 15.6" i5-7300HQ
* macOS or windows PC to create the install USB
* 8GB or larger USB stick (USB3 preferred for speed)
* **Internet Connection** if you create install drive using [gibMacOS](https://github.com/corpnewt/gibMacOS/archive/master.zip)
* Latest copy of this repo
* (optional for multiboot) Second (PCI M.2) SSD installed inside the laptop.
* (possibly) USB mouse for install until trackpad is working

| Working | Not working |
| ------------- | ------------- |
| [Wifi Intel]() (buggy, try restart or clear nvram) | * Nvidia GPU (Disabled since 1050Ti was under Optimus)  |
| [Wifi Intel Gui](https://github.com/1hbb/OpenIntelWireless-Factory/releases) | Card Reader |
| Intel Graphics HD 630 | Battery Management |
| FN brightness adjustment (SSDT-FN.aml Fix By [shomerchang](https://github.com/shomerchang)) | Trackpad (gestures) |
| USB 3.0 | Sleep/Wake |
| Audio, ALC1220 (Using AppleALC) | HDMI Video and Audio |
| Built-in camera |  |
| Built-in mic | |
| NVMe / SATA SSD's |  |
| Native CPU Power Management |
| Bluetooth Intel (hvnt test for Handsoff/Airdrop/etc) |

***

## Installation
Downloading macOS:
* Download [gibMacOS](https://github.com/corpnewt/gibMacOS/archive/master.zip) from https://github.com/corpnewt/gibMacOS/
* Extract it somewhere and run gibMacOS.bat
* Choose your desired macOS version by entering the number and pressing the ENTER key.
* macOS will now download, grab a coffee.
* Once the download is finished you can exit the program with the keys Q then ENTER

Making the installer USB stick:
* Insert your USB stick
* Now run MakeInstall.bat **as Administrator**
* **IMPORTANT:** In the next step it's important to choose the correct disk, the risk of deleting all the files on that pc are very high! Choose only your USB stick!
* Enter the number of your USB stick and hit ENTER, then type Y and hit ENTER (All files on your USB stick will be deleted!)
* Now go to the 'macOS Downloads\publicrelease' folder inside the 'gibMacOS' folder
* Hold the Shift key and right-click the macOS folder that you want to install on the USB stick and click **Copy as path**
* Go back to the MakeInstall.bat program and right-click in the window to paste the file path, then hit ENTER
* Your USB stick will be created, have a second coffee.
* When it's finished, close the program.

Making the USB stick Xiaomi compatible:
* Download the latest version of this repo
* Extract it somewhere
* Open the BOOT drive from the Windows explorer (usually drive D:, E: or F:)
* Replace the EFI folder on the BOOT drive with the EFIOC (opencore) folder you just downloaded from this website.
* Eject the USB stick and insert into Xiaomi laptop.

Installing macOS:
* Now reboot and Press F12 to boot from USB (if trackpad is not working, use USB mouse.)
* Open Disk Utility and format your desired SSD with APFS (will delete all your files!!!)
* Install macOS 
* After install, Press F12 ti boot from USB again 
* Select the drive you installed in the Opencore Bootloader (Should say macInstaller)
* Do initial macOS setup (Internet needed)
* Mount the ESP (EFI System Partition) on your drive (check that you mount the correct EFI partition, **numbers will vary!!!**)
```
diskutil list
sudo diskutil mount /dev/disk0s1
```
* Copy the EFI on your USB to the mounted drive
* Remove the USB stick from the laptop
* Done! Reboot to enable all the kexts. Enjoy your Hackintosh!

## Optional
[Fixing iServices](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/extras/iservices)
[BIOS Modification](https://github.com/johnnync13/XiaomiGaming)

***

# Credits
- [johnnync13](https://github.com/johnnync13/) origin repo

- [yllwfsh](https://github.com/yllwfsh) for maintenance, fix issues and create a good friendly README

- [xzhih](https://github.com/xzhih) For the excellent [hidpi](https://github.com/xzhih/one-key-hidpi) script.

- [stevezhengshiqi](https://github.com/stevezhengshiqi) He is a good developer. I'm learning a lot about how to patch problems. Thanks for PCIList.aml and more.

- [RehabMan](https://github.com/RehabMan) Updated [OS-X-Clover-Laptop-Config](https://github.com/RehabMan/OS-X-Clover-Laptop-Config) and [Laptop-DSDT-Patch](https://github.com/RehabMan/Laptop-DSDT-Patch) and [OS-X-USB-Inject-All](https://github.com/RehabMan/OS-X-USB-Inject-All) for maintenance

- [vit9696](https://github.com/vit9696) Updated [Lilu](https://github.com/vit9696/Lilu) and [AppleALC](https://github.com/vit9696/AppleALC) and [WhateverGreen](https://github.com/vit9696/WhateverGreen)  for maintenance

- [alexandred](https://github.com/alexandred) Updated [Voodooi2c](https://github.com/alexandred/VoodooI2C) for maintenance

- [Community Chinese](https://github.com/a565109863) Updated [Intel Wifi](https://bbs.pcbeta.org/forum.php?mod=viewthread&tid=1838489) for intel wifi and tutorial
