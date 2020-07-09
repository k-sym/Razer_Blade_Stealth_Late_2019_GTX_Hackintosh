# Razer Blade Stealth late 2019 macOS 10.15 Hackintosh

**Note: I AM NOT RESPONSIBLE IF YOU MESS UP YOUR COMPUTER USING THIS GUIDE!**

SUPPORT
---
**I am by no means an expert and would welcome advice on how to improve. I'm open for any cooperation and will try maintain this repository as much as possible. Please fill free to create Pull Requests.**

Intro
---

![About this Mac](https://github.com/ksymmonds/Razer_Blade_Stealth_Late_2019_GTX_Hackintosh/blob/master/img/about_this_mac.png)

I have been using Apple hardware and software since the mid 90's and it's has been the best OS to meet my needs. I've had an MBP (15", 2017) for the last few years but for various reasons, have not been 100% happy. I've Hackintoshed a few PC laptops in the early days, borne mainly out of my love of Linux and my most resent success was with a Razer Blade Advanced 2019 using the excellent [StoneEvil](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh) guide. Whilst an excellent machine, it's just a tad too big for my needs, so decided to go the Stealth route. The following catalogues my pains to get this to the same level as my old Blade 15 Advanced.

**Purpose**

* Cloud and DevOps.
* iOS development.
* Infrequent gaming.
	* [PUBG](https://pubg.com/en-us)
	* [GTA series](https://www.rockstargames.com/games/info/V)
    * [Rebel Galaxy Outlaw](https://rebel-galaxy.com/)


Hardware
---

**Razer Blade Stealth late 2019 GTX**

| Item | Spec | Working |
| ---: | :--- | :--- |
| ``CPU`` | Quad-Core 10th Gen Intel® Core™ i7-1065G7 Processor with Hyper-Threading 1.3 GHz / 3.9 GHz (Base/Turbo) | Yes |
| ``Memory`` | 16GB LPDDR4 3733MHz dual-channel onboard memory (Fixed)| Yes |
| ``GPU`` | Intel UHD Iris Plus | Not yet |
| ``dGPU`` | NVIDIA® GeForce® GTX 1650 4GB GDDR5 VRAM | No dirvers for this card. ACPI should be patched to disable dGPU |
| ``Storage`` | 256GB PCIe M.2 | Yes |
| ``Screen`` | 13.3" FHD Matte (1920 X 1080), 100% sRGB, 4.9mm slim side bezels | Yes (although shows as a projector?) |
| ``Webcam`` | Webcam (720P) |  Yes. Windows Hello is not supported in macOS |
| ``WiFi`` | Intel Wireless-AC 9560NGW | Drivers absent for macOS. Should replaced |
| ``Input & Output`` | USB-C 3.1 Gen 2, power port 2x Type-A USB 3.1| Yes |
| ``Thunderbolt 3 (USB-C)`` | Yes |
| ``Soundboard`` | Realtek ALC298 | Not yet |
| ``Battery`` | 53Wh | No |
| ``Keyboard`` | Keyboard with Razer Chroma™ single-zone full key backlighting | Yes |
| ``Touchpad`` | Precision Glass | Not yet |

**Full Official Spec list here : [Razer](https://support.razer.com/gaming-laptops/razer-blade-stealth-13-late-2019-gtx-model/)**


Hardware Upgrades and Tools
---

The bundled ``WiFI`` and ``NVMe`` is not compatible with macOS and should be replaced. I replaced my Wifi / BT card with a Broadcom (DW-1560) and the SSD was replaced by a DataRAM 1TB NVME card.


**Accessories**

| Accessories | Description |
| ---: | :--- |
| ``USB mouse`` | Trackpad will be unavailable during macOS installation procedure |
| ``USB storage`` with at least 16Gb storage | Installation USB media | 


**WiFi**

| WiFi module | Description |
| ---: | :--- |
| ``BCM94352Z (DW-1560)`` | Recommended. 2 antennas. No issues. Additional kext's are required. Easily to find for \$24-60 on |
| ``BCM943602BAED (DW-1830)`` | 3 antennas. RBA have only 2. Works out of the box. |

Repository
---
``ACPI`` directory. This contains all the decompiled '.aml' files for review.

``OC`` directory. This is my current working 'OC' directory within my EFI directory.

``img`` directory. Images use in this ReadMe and also screenshots that support ACPI alterations. 


Method
---
* Create the install media
* Collect and compile the ACPI files
* Collect the kext's needed
* create the config.plist
* Install OSX
* Copy the EFI onto your bootable drive
* Post Install setups


**Create the install media**

So, I'm lucky enough to have a Mac already, so these instructions are based on this fact.

I followed the instructions detailed [here](https://dortania.github.io/vanilla-laptop-guide/preparations/offline-installer.html) and downloaded the installer files using [gibMacOS](https://github.com/corpnewt/gibMacOS) and creating the packages. Prep your USB drive and create the Installer USB using the 'createInstallmedia' command.

`sudo /path/to/installer-app/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyNewlyFormattedUSB`

After creation, copy the OpenCore EFI files over. I followed [this](https://dortania.github.io/vanilla-laptop-guide/preparations/opencore-efi.html) guide. The result can be found in the [`OC`](https://github.com/ksymmonds/Razer_Blade_Stealth_Late_2019_GTX_Hackintosh/tree/master/OC) folder of this repo.


ACPI files
---

Folowing on from the install media, the ACPI files were next. Using the guide, we see that we need these SSDT's.

![ACPI Table](https://github.com/ksymmonds/Razer_Blade_Stealth_Late_2019_GTX_Hackintosh/blob/master/img/acpi-table.jpg)


**CPU**

First up, CPU power management.

![Device Manager CPU](https://github.com/ksymmonds/Razer_Blade_Stealth_Late_2019_GTX_Hackintosh/blob/master/img/acpi-cpu.jpg)

The Blade Stealth (according to Device Manager in Windows) has the ACPI path of `_SB.PR00` (up to 07) so we can remove all but this reference in the SSDT-PLUG.dsl and then compile.

**Embedded Controller**

Next, the embedded controller.

![Device Manager EC](https://github.com/ksymmonds/Razer_Blade_Stealth_Late_2019_GTX_Hackintosh/blob/master/img/acpi-ec.jpg)

So, back in the Windows Device Manager, the EC is shown as `_SB.PCI0.LPCB.EC0`. However, this Blade DOES fall into an Edge case as outlined [here](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-methods/manual.html#pnp0c09-already-has-an-sta-method)

As shown in the DSDT dump from the Blade:

![EC Edge Case](https://github.com/ksymmonds/Razer_Blade_Stealth_Late_2019_GTX_Hackintosh/blob/master/img/acpi-ec-edge.jpg)

So we don't actually need a `SSDT-EC.aml`, but as the Blade is a newer than SkyLake, we still need the `SSDT-USBX.aml` for USBX.

**Backlight**

Next, the backlight. I'll go through this process, however we know already that there are issues (currently) with the [Mobile Icelake](https://github.com/dortania/bugtracker/issues/17) chipset...

Back to Windows Device Manager, we find the ACPI path name for the device:

![EC Edge Case](https://github.com/ksymmonds/Razer_Blade_Stealth_Late_2019_GTX_Hackintosh/blob/master/img/acpi-backlight.jpg)







