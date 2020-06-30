# Razer Blade Stealth late 2019 macOS 10.15 Hackintosh

**Note: I'AM NOT RESPONSIBLE IF YOU MESS UP YOUR COMPUTER USING THIS GUIDE!**

SUPPORT
---
**I by no means an expert and would welcome advise on how to improve. I'm open for any cooperation and will try maintain this repository as much as possible. Please fill free to create Pull Requests.**

Intro
---

![About this Mac](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/About_Mac.png)

I have been using Apple hardware and software since the mid 90's and it's has been the best OS to meet my needs. I've had an MBP (15", 2017) for the last few years but for various reasons, have not been 100% happy. I've Hackintoshed a few PC laptops in the early days, borne mainly out of my love of Linux and my most resent success was with a Razer Blade Advanced 2019 using the excellent (https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh) StoneEvil guide. Whilst an excellent machine, it's just a tad too big for my needs, so decided to go the Stealth route. The following catalogues my pains to get this to the same level as my old Blade 15 Advanced.

**Purpose**

* Cloud and DevOps.
* iOS and macOS development.
* Gaming maybe once per month. Usually 3A titles like
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
| ``GPU`` | Intel UHD Iris Plus | No |
| ``dGPU`` | NVIDIA® GeForce® GTX 1650 4GB GDDR5 VRAM | No dirvers for this card. ACPI should be patched to disable dGPU |
| ``Storage`` | 256GB PCIe M.2 | Yes |
| ``Screen`` | 13.3" FHD Matte (1920 X 1080), 100% sRGB, 4.9mm slim side bezels |  No issues |
| ``Webcam`` | Webcam (720P) |  Yes. Windows Hello is not supported in macOS |
| ``WiFi`` | Intel Wireless-AC 9560NGW | Drivers absent for macOS. Should replaced |
| ``Input & Output`` | USB-C 3.1 Gen 2, power port 2x Type-A USB 3.1| Yes |
| ``Thunderbolt 3 (USB-C)`` | Yes |
| ``Soundboard`` | Realtek ALC298 | No |
| ``Battery`` | 53Wh | No |
| ``Keyboard`` | Keyboard with Razer Chroma™ single-zone full key backlighting | Yes |
| ``Touchpad`` | Precision Glass | No |

**Full Official Spec list here : [Razer] (https://support.razer.com/gaming-laptops/razer-blade-stealth-13-late-2019-gtx-model/)**


Hardware Upgrades and Tools
---

The bundled ``WiFI`` and ``NVMe`` is not compatible with macOS and should be replaced. I replaced my Wifi / BT card with a Broadcom (DW-1560) and the SSD was replaced by a DataRAM 1TB NVME card.


**Accessories**

| Accessories | Description |
| ---: | :--- | :--- |
| ``USB mouse`` | Trackpad will be unavailable during macOS installation procedure |
| ``USB storage`` with at least 16Gb storage | Installation USB media | 


**WiFi**

| WiFi module | Description | eBay or AliExpress URL | Confirmation |
| ---: | :--- | :--- | :--- |
| ``BCM94352Z (DW-1560)`` | Recommended. 2 antennas. No issues. Additional kext's are required. Easily to find for \$24-60 on | [eBay](https://www.ebay.com/sch/i.html?_from=R40&_nkw=BCM94352Z+DW-1560&_sacat=0&rt=nc&LH_BIN=1) | [community](https://osxlatitude.com/forums/topic/11138-inventory-of-supportedunsupported-wireless-cards-2-sierra-catalina/) |
| ``BCM943602BAED (DW-1830)`` | 3 antennas. RBA have only 2. Works out of the box. About \$60-120 on AliExpress | [AliExpress](https://www.aliexpress.com/wholesale?catId=0&initiative_id=SB_20190707194727&SearchText=BCM943602BAED+DW1830&switch_new_app=y) | [community](https://osxlatitude.com/forums/topic/11138-inventory-of-supportedunsupported-wireless-cards-2-sierra-catalina/) |

Repository
---
``ACPI`` directory. This contains all the decompiled '.aml' files for review.

``OC`` directory. This is my current working 'OC' directory within my EFI directory.
