---
published: true
title: Gigabyte Z270 Gaming Ultra Hackintosh Build Guide
layout: post
---
This build will walk you through the process of turning you Gigabyte's high end Z270 Gaming Ultra Motherboard into a everyday-driver-usable Hackintosh machine. The motherboard works well in Hackintosh except that I haven't been able to get the audio working with any other kext than Voodoo. A reminder to toss in an SSD into this build if you want it to be usable, macOS on HDDs can be slow.

I have already prepared an EFI folder so you don't have to go through the complicated steps of figuring out which kexts to use and how compatible are some compared to the others. Here's the list of all the kexts used in this build

- ACPISensors.kext
- CPUSensors.kext
- FakeSMC.kext
- GPUSensors.kext
- IntelMausiEthernet.kext (for Mobo Ethernet)
- LPCSensors.kext
- USBInjectAll.kext (to make USB 3 work)
- XHCI-200-series-injector.kext ( dependency of USBInjectAll )

While the sensors kexts are optional, they are highly recommended if you use programs such as iStatsMenu.

## Setting up your Hackintosh

The first thing you're gonna need is a USB disk to install macOS High Sierra on, You could follow the OSXDaily's guides to [downloading the public beta][2] and [making a bootable mac USB Drive][3].

You do NOT need to disable Vt-d or FastBoot as some guides recommend. If you have an AMD GPU (think RX series) you will have to set the initial display output to iGPU in your bios and plug in your monitor to the mobo display output. After macOS boots up you can plug it into the GPU display socket or switch the display input (if your monitor supports more than one).

Work is underway on solving this for AMD GPU users using the [WhateverGreen.kext][4] but I did not find it stable enough to use everyday as it's display lags at around 30hz at the time of writing.

Next up is downloading the [`EFI.zip`][5] with preconfigured Clover that supports APFS and unzipping it into your USB.

Lastly reboot into the USB and proceed with macOS installation.

## Useful Links

- [r/hackintosh](https://www.reddit.com/r/hackintosh/)
- [r/hackintosh Discord](https://discord.gg/u8V7N5C)

**Update**: The [WhateverGreen.kext][4] mentioned above has become stable enough to be a daily driver, you should include it in your kexts folder (`EFI/CLOVER/kexts/Other/`) if you are using an AMD GPU


[1]:https://developer.apple.com/download/
[2]:http://osxdaily.com/2017/06/29/download-install-macos-high-sierra-public-beta/
[3]:http://osxdaily.com/2017/06/12/make-boot-macos-high-sierra-beta-install-drive-usb/
[4]:https://github.com/vit9696/WhateverGreen
[5]:https://1drv.ms/u/s!Aq4tygM5KOP7hHmtnQ7ji63zV6ls
