---
layout: post
title: Chromebook Pixel (2015)
comments: true
summary: How I am happily productive on a Chromebook Pixel.
---

## Overview

In my opinion the greatest device Apple has created to date, is their Macbook Air. I was a proud owner of a 13" MBA and used it for entertainment, learning and development. However, as the device aged, and the new models lacked features I wanted, I started looking elsewhere for a replacement. I decided to go with the unorthodox Chromebook Pixel LS. Unlike the MBA, the Pixel takes quite a bit more setup to become productive. This extra work ultimately leads to a more enjoyable experience. This post will outline the setup and tools I use on the Pixel to be productive and happy.

## Apps

Obviously with a Chromebook you have access to the entire web and thus tons of awesome productivity websites. I won't list my favourite sites here, but instead list a couple Chrome specific apps.

#### <a href="https://chrome.google.com/webstore/detail/caret/fljalecfjciodhpcledpamjachpmelml?hl=en">Caret</a>

Caret is a fantastic little text editor that is based off of <a href"https://github.com/ajaxorg/ace">ace</a>. It can be run completely offline and has syntax highlighting for tons of languages. My favorite feature is that it has a built in VIM mode for key bindings.

#### <a href="https://chrome.google.com/webstore/detail/3dview/hhngciknjebkeffhafnaodkfidcdlcao?hl=en">3dview</a>

3DView is an easy to use application for viewing 3d models in various file formats. I use it to quickly inspect STL downloads from Thingiverse.

#### <a href="https://chrome.google.com/webstore/detail/videostream-for-google-ch/cnciopoikihiagdjbjpnocolokfelagl?hl=en">Videostream</a>

I used to use Beamer, a fantastic streaming app for OS X. These days most of my streaming content is viewed through a Chromecast. Videostream allows you to cast your own local videos in almost any format. Note to get it to work on your Pixel you must execute the following commands in your <a href="https://www.chromium.org/chromium-os/poking-around-your-chrome-os-device">developer shell</a>:


{% highlight bash %}
sudo /sbin/iptables -A INPUT -p tcp --dport 5556 -j ACCEPT

sudo /sbin/iptables -A INPUT -p tcp --dport 5558 -j ACCEPT
{% endhighlight %}

## Crouton

Crouton is a set of scripts that bundle up into an easy-to-use, Chromium OS-centric chroot generator. Essentially it allows you to sideload popular Linux distributions on your Chromebook. You'll be able to flip between OS's with a simple key press or even run Linux applications while using Chrome OS's window manager. There are tons of great how-to's on the installation process so I won't walk through it here. However, there are a couple extra concerns for the Pixel that I will outline.

#### Resolution

The hiDPI screen of the Pixel causes issues with certain Linux distributions. In fact there is a specific <a href="https://github.com/dnschneid/crouton/wiki/Chromebook-Pixel">section</a> of the Crouton github dedicated to solutions. I've personally found great success with Ubuntu 14.04 and simply setting the scale factor to 2 under display settings. Most apps respond as expected and everything remains ultra crisp.

#### Intel Drivers

If you don't update your Intel drivers the switching back and forth between Chrome OS and Ubuntu can cause screen tears and mouse rendering issues. Simply execute the following commands in your terminal to update the drives.

{% highlight bash %}
sudo apt-get install software-properties-common python-software-properties

sudo add-apt-repository https://download.01.org/gfx/ubuntu/14.04/main

wget --no-check-certificate https://download.01.org/gfx/RPM-GPG-KEY-ilg -O - | sudo apt-key add -

wget --no-check-certificate https://download.01.org/gfx/RPM-GPG-KEY-ilg-2 -O - | sudo apt-key add -

sudo apt-get update

sudo apt-get upgrade
{% endhighlight %}

#### Touchpad Drivers

The default synaptic drivers that come with Ubuntu work well enough but I prefer the X11 ChromiumOS drivers ported to Linux. Execute the following commands to install the drivers.


{% highlight bash %}
sudo add-apt-repository ppa:hugegreenbug/cmt

sudo apt-get update

sudo apt-get install -y libevdevc libgestures xf86-input-cmt

sudo mv /usr/share/X11/xorg.conf.d/50-synaptics.conf /usr/share/X11/xorg.conf.d/50-synaptics.conf.old

sudo cp /usr/share/xf86-input-cmt/50-touchpad-cmt-<model>.conf /usr/share/X11/xorg.conf.d/
{% endhighlight %}

#### Drive

Chromebooks typically come with a significant amount of Google Drive space. Using this space from Crouton can be a bit of a pain as there is not an easy way to mount your drive as a normal directory. To make your drive somewhat more useable from Linux is an aptly named tool called <a href="https://github.com/odeke-em/drive">Drive</a>. This tiny program allows you to pull or push Google Drive files.

## Tips and Tricks

#### Crouton Backup

Crouton has a built in command to allow backups. As mentioned earlier, most Chromebooks come with a ton of free Google Drive space. I have been storing my backups with great success on Drive. Uploads were fast and painless using the default Files app on Chrome OS.

#### Chrome-OS APK

<a href="https://github.com/vladikoff/chromeos-apk">Chrome-os apk</a> is a great little Node tool to package apk's into extensions that can be run in Chrome. I have tested a handful of Android applications with great success. With the Pixel's touch screen, apps are extremely easy to use and run extremely smooth. Don't forget to add the '--tablet' parameter when using the tool.
