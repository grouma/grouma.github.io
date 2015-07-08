---
layout: post
title: Duplicator I3
comments: true
summary: Initial thoughts on the Duplicator I3 3d printer.
---

### Overview

Although I have been researching 3d printers for some time, I have been too apprehensive to purchase one. The overwhelming amount of choice and the non-trivial cost made it very difficult to select a model. Moreover, not knowing what features were absolutely critical to a pleasant printing experience made the task absolutely daunting. That's why when I stumbled across the <a href="http://wanhaousa.com/products/duplicator-i3-steel-frame">Duplicator i3</a>, which has a laundry list of features, at an absolutely insane price of $375 (shipped!) I couldn't say no.

### Features

* Heated print bed
* Large print area: 200mm x 200mm x 180mm
* Sturdy steel construction
* Compatible with many filaments: PLA, ABS, PVA etc.
* 100 micron layer capability
* Open design
* File printing
* Includes flash card, USB cable and putty scraper
* Assembled

### Delivery

I have been following the Duplicator I3 <a href="https://groups.google.com/forum/#!forum/wanhao-printer-3d">forums</a> and unfortunately the first batch of printers had a lot of issues. Folks were complaining about devices being damaged beyond repair during shipment. This was such an issue that the manufacturer, Wanhao, had to delay printers to revise the packaging. I must commend them though as they quickly resolved the issue and only introduced a week's delay in shipping time. Since I purchased my printer on the last day of the presale, I lucked out and received a printer with revised packaging. Besides some minor cosmetic scratches to the print bed, my device was received in perfect working order.

### Setup

The printer is advertised as being assembled, however there is some minor setup required by the end user. I was able to setup the printer in about 15 minutes without instructions. Note that there are instructions on the provided flash card, something I was not aware of. I recommend looking at them as I made the silly error of connecting the x-axis cable to the z-axis motor. Luckily I corrected the mistake before any serious damage could be done.

One major feature missing on this printer is a z-probe which allows for automated bed leving through software. Since this printer does not have one, you must manually level by tightening or loosening screws on the four corners of the print bed. Speaking as a novice, this process is a bitch. I watched several YouTube videos describing the leveling process but in the end I had to do a lot of trial and error to get the correct adjustment.

### Print Quality

The first object I printed was the provided hand model on the included flash drive. This model came presliced with what I assumed optimized settings for the Duplicator I3. I was in a rush to get the printer started so I hastily leveled the bed, which in hindsight was way too close. Regardless I think the print turned out fantastic as you can see below.
![ok](/public/images/hand.JPG)

Since printing the provided sample, I have been in the process of optimizing my slicer settings. I was initially using <a href="https://ultimaker.com/en/products/cura-software">Cura</a> directly. I have since switched to using <a href="https://www.astroprint.com/dashboard">Astroprint</a> which provides free online slicing. It has fantastic defaults and has resulted in some great prints. See the Octopus print below.
![octopus](/public/images/octopus.JPG)

Overall I'm blown away by the print quality, without even considering the price. I look forward to dialing in the settings and printing custom parts. As for creating models, I have been using <a href="http://www.openscad.org/">OpenSCAD</a> which I highly recommend.

### Future Modifications

My employer, Google in Seattle, has a dedicated maker space with several printers. One of their printers has a Borosilicate glass print bed. This allows the user to forgo the standard practice of covering the print bed with blue painter's tape. This of course makes for an easier setup and cleaning, but also results in better print quality as the printed object will have a perfectly smooth base. I plan on adding a sheet of this glass to my print bed as well.

The Duplicator I3 has the capability of printing from a flash drive, which is great as printing does occupy your computer. However, monitoring your print requires you to be directly in front of the device. I plan on purchasing a Raspberry Pi and modifying the printer to use <a href="http://octoprint.org/">Octoprint</a>. This will allow me to initiate prints and monitor them remotely.
