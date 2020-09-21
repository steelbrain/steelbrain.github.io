---
published: true
title: What I learned flashing an EEPROM
layout: post
---

### Context:

I used to travel with two laptops, a gaming laptop and a macbook for work on the go. I couldn't carry a single laptop for both tasks in the past because I needed 4k for design work and a fast refresh rate display for smooth gaming. I recently upgraded to a Razer Blade Pro 17 2020 to fulfill this goal, it boasts a 4k 120hz OLED Touch Display. I needed some BIOS configurations to make it work for my usecase. The BIOS came locked on this machine by the manufacturer so I had to reflash the BIOS with a hardware programmer.

### What I used:

I used a CH341A USB programmer on Windows paired with ASProgrammer. Instead of desoldering the BIOS from the Laptop Mobo and resoldering it on the programmer and back, I used the SOIC8 SOP8 Test Clip. You may want to order more than one as the first one I tried turned out to be faulty.

### What I learned from this experience:

- If your machine boots, use that as an opportunity to extract as much information as you can about the BIOS you're about to flash. The programmer needs to know the exact model, otherwise the flashing won't work. Most programmers have a chip-detection feature but it can be spotty.
- Download a BIOS update from the manufacturer, and dump the BIOS from the cip. Make sure that they both have the same size. Most BIOS update executables from manufacturers can be unzipped to extract the BIOS fw.
- Make sure to erase the BIOS before writing. If you just dump and write, the programmer will skip over the zero-bytes leaving you with a corrupt BIOS fw. Some programmers have an erase-flash-verify feature, use that if you can.
- Practice on a dual-BIOS Computer Motherboard if you can, that'll greatly lower your chances of failure in your first attempt.
