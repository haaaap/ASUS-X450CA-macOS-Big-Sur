# OpenCore 0.7.6 files for Asus X450CA running macOS Big Sur 11.6.2
NOTICE: **This OpenCore EFI files does not have a SMBIOS. Generate and add your smbios (MacBookAir6,2) with the [GenSMBIOS tool](https://github.com/corpnewt/GenSMBIOS).**
## What's Working?
- Boot
- Hardware Acceleration
- Audio Input & Output
- USB 2.0 Mapping
- WebCam
- Brightness Control
- Trackpad (Settings accessible with battery installed)
- Ethernet 
- HDMI Port, _with audio Output!_
- iServices (**WITH PROPER SMBIOS CONFIGURATION.**)
- Headphone Jack
- USB Tethering with [HoRNDIS](https://github.com/jwise/HoRNDIS/)
- sleep/wake, fn+f1 keyboard combo works too!

## What Doesn't Work?
- WiFI (macOS does not support Atheros cards natively, you can try to use [ATH9KFixup](https://github.com/black-dragon74/ATH9KFixup "Atheros 9K series wifi fix") to fix it)
- VGA Port
- Internal Card Reader
- USB 3.0 Speeds

## Weird Quirks and Shit I need to fix
- Phase 1 boot is stretched, could be firmware limitation
- screen glitching at boot phase transition, non issue for me
- haven't set up OC Boot Picker as i don't need it
- USB 3.0 Mapping
- fn key support is available with [Karabiner-Elements](https://karabiner-elements.pqrs.org/)
- pressing fn+f8 (Projector button thing) on lock screen, or w/o Karabiner-Elements **COMPLETELY SHITS YOUR DISPLAY, DO NOT RECCOMEND.**

## BIOS Settings
- DVMT-PRE-ALLOC: 64M

## How to actually install macOS Big Sur?
- acquire files
  - macOS Recovery Files with macrecovery.py (found in `Tools` folder)
  - EFI files
- appropriate installation medium (refer to "Creating the USB" part on [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/))
- copy in files
- Create SMBIOS data for MacBookAir6,2 with GenSMBIOS (found in `tools` folder)
  - make sure that the s/n is not [registered](https://checkcoverage.apple.com)
- fill in SMBIOS data on PlatformInfo/Generic
- example of SMBIOS data and where to fill it in
`
Type:         MacBookAir6,2 
Serial:       C02PK0NZF5V7 (for SystemSerialNumber) 
Board Serial: C02515501J9FD47CB (for MLB)
SmUUID:       D5444EFD-4362-49DC-A1B4-7159BD1D508F (for SystemUUID)
Apple ROM:    1093E9653261 (for ROM)
`
- boot computer, spam f2, select `(UEFI) flashdisk name`
- computer should boot into macOS recovery
- make sure you have ethernet
- nuke hard disk, install macos
- computer would reboot a few times during reboot, choose `macOS Installer`
- finish installation, then use mountEFI to well, "mount efi"
- copy EFI files into local hard disk, remove anything inside in the process
- reboot into BIOS, add Boot Option with the path 

## Credits
- The [Acidanthera](https://github.com/acidanthera/) team for the OpenCore bootloader, AppleALC, lilu, WhatEverGreen, VirtualSMC, VoodoooPS2Controller.kext,
- [jwise](https://github.com/jwise) For HoRNDIS.kext,
- [RehabMan](https://github.com/RehabMan) For Various DSDT Patches,
- [Mieze](https://github.com/Mieze) For RealtekRTL8111.kext,
- [1Revenger1](https://github.com/1Revenger1) For ECEnabler.kext,
- [corpnewt](https://github.com/corpnewt) For USBMap tool, and GenSMBIOS
- The [/r/Hackintosh Paradise](https://discord.gg/Wxam8aH) Discord Server for helping me clean up *most* of the weird quirks
