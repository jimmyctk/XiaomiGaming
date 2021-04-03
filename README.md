![GitHub release](https://img.shields.io/github/release/johnnync13/XiaomiGaming.svg)

# Disclaimer!
This is a fork from [johnnync13] https://github.com/johnnync13/XiaomiGaming and I am just porting for the Xiaomi Gaming Book 7th gen with KabyLake. I do not own any copyright.
Use these files and this howto at your own risk. I'm not responsible in any way for lost data, damage to software or hardware or anything else that might go wrong. This works for me but might not for you.

# EFI Folder for the Xiaomi Gaming 7th Generation (KabyLake)

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

### 
| Working | Not working |
| ------------- | ------------- |
| [Wifi Intel]() (buggy, try restart or clear nvram) | * Nvidia GPU (Disabled since 1050Ti was under Optimus)  |
| [Wifi Intel Gui](https://github.com/1hbb/OpenIntelWireless-Factory/releases) | Bluetooth Intel |
| Intel Graphics HD 630 | Card Reader |
| FN brightness adjustment (SSDT-FN.aml Fix By [shomerchang](https://github.com/shomerchang)) | Brightness keys|
| USB 3.0 | Sleep/Wake |
| Audio, ALC1220 (Using AppleALC) | Native CPU Power Management |
| Built-in camera | Battery Management |
| Built-in mic | Trackpad (gestures) |
| NVMe / SATA SSD's | HDMI Video and Audio |

### Installation
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
* Mount the ESP (EFI System Partition) on your drive (check that you mount the correct EFI partition, numbers will vary!!!)
```
diskutil list
sudo diskutil mount /dev/disk0s1
```
* Copy the EFI on your USB to the mounted drive
* Remove the USB stick from the laptop
* Done! Reboot to enable all the kexts. Enjoy your Hackintosh!

# macOS is working! Next steps:
### (optional) Fixing iMessage, FaceTime etc.
This can be a bit of a challenge, and outside of the scope of this repo, but if you want to, have a look here:<br />
[An iDiot's Guide To iMessage (clover)](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/)<br />
[Fixing iServices (OpenCore)](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/extras/iservices)

***

# BIOS Modification
* [johnnync13] suggested we should modify the BIOS, will try later. It is really important on OpenCore, that the laptop have unlocked CFG Lock. It is important to CPU, sleep/wake and better behavior like native macOS. It is very easy on the most laptops because the BIOS has option in menu, but no on Xiaomi BIOS.

### Tutorial to modify BIOS  
* I would like make a script or others methods but this tutorial is like OpenCore method.  
* Soon I upload a csv with all xiaomi laptops that I have on the github with hexadecimal variables to unlock CFG Lock, MC Lock, SpeedShift and more.    
* ## THIS TUTORIAL IS AN EXAMPLE, NOT GET THE VALUES AND VARIABLES
  
## First of all, I am not responsible for what can happen to your laptop  
  
1- Boot with OpenCore  
2- Click on space key on keyboard.  
3- Select partition Mod Grub Shell  
4- Write a command method, for example to unlock cfg lock: setup_var 0x3C 0x00  
Other example, SpeedShift to enable: setup_var 0xB 0x01  
it is possible that for example, SpeedShift is enabled before.     
* ### Explanation:  
setup_var is to call method function.  
0x3C is the location memory on bios that is variable CFG Lock.    
0x00 is to disable and 0x01 is to enable. I put the example here.  
(default) is how the variable is when you install a BIOS, that is, by the manufacturer.  

One Of: CFG Lock, VarStoreInfo (VarOffset/VarName): 0x3C, VarStore: 0x3, QuestionId: 0x146, Size: 1, Min:   0x0, Max 0x1, Step: 0x0 {05 91 8A 02 8B 02 46 01 03 00 3C 00 10 10 00 01 00}  
0x149413 			One Of Option: Disabled, Value (8 bit): 0x0 {09 07 04 00 00 00 00}  
0x14941A 			One Of Option: Enabled, Value (8 bit): 0x1 (default) {09 07 03 00 30 00 01}  
0x149421 		End One Of {29 02}  
  
5- You can set up more variables to modify Bios. If you want exit, you must write reboot and click enter on keyboard.  
  
6- You can verify the CFG is unlocked or other parametres like SpeedShift is enabled in hackintool, section Utilities and press button Get AppleIntelInfo.  

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
