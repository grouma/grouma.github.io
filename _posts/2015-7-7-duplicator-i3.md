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


### Print Video

<blockquote class="instagram-media" data-instgrm-captioned data-instgrm-version="4" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:658px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:8px;"> <div style=" background:#F8F8F8; line-height:0; margin-top:40px; padding:50% 0; text-align:center; width:100%;"> <div style=" background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAsCAMAAAApWqozAAAAGFBMVEUiIiI9PT0eHh4gIB4hIBkcHBwcHBwcHBydr+JQAAAACHRSTlMABA4YHyQsM5jtaMwAAADfSURBVDjL7ZVBEgMhCAQBAf//42xcNbpAqakcM0ftUmFAAIBE81IqBJdS3lS6zs3bIpB9WED3YYXFPmHRfT8sgyrCP1x8uEUxLMzNWElFOYCV6mHWWwMzdPEKHlhLw7NWJqkHc4uIZphavDzA2JPzUDsBZziNae2S6owH8xPmX8G7zzgKEOPUoYHvGz1TBCxMkd3kwNVbU0gKHkx+iZILf77IofhrY1nYFnB/lQPb79drWOyJVa/DAvg9B/rLB4cC+Nqgdz/TvBbBnr6GBReqn/nRmDgaQEej7WhonozjF+Y2I/fZou/qAAAAAElFTkSuQmCC); display:block; height:44px; margin:0 auto -44px; position:relative; top:-22px; width:44px;"></div></div> <p style=" margin:8px 0 0 0; padding:0 4px;"> <a href="https://instagram.com/p/4xLoE6kzSb/" style=" color:#000; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none; word-wrap:break-word;" target="_top">Starting to get things calibrated nicely. #3dprinting #octopus for @amadera711</a></p> <p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;">A video posted by Gary Roumanis (@grouma) on <time style=" font-family:Arial,sans-serif; font-size:14px; line-height:17px;" datetime="2015-07-05T20:49:28+00:00">Jul 5, 2015 at 1:49pm PDT</time></p></div></blockquote>
<script async defer src="//platform.instagram.com/en_US/embeds.js"></script>
