---
title: Sensor IoT Workshop
date: 2019-03-18 15:00:00 
categories:
- education
tags: raspberry-pi IoT
layout: post
thumbnail: "/images/rpi.png"
excerpt: Getting Started with the Raspberry Pi
---

# Raspberry Pi

![alt text](/images/rpi.png)



The Raspberry Pi is a series of small single-board computers developed in the United Kingdom by the Raspberry Pi Foundation to promote the teaching of basic computer science in schools and in developing countries. The original model became far more popular than anticipated, selling outside its target market for uses such as robotics.

The Raspberry Pi Foundation provides Raspbian, a Debian-based Linux distribution for download, as well as third-party Ubuntu, Windows 10 IoT Core, RISC OS, and specialised media centre distributions.[109] It promotes Python and Scratch as the main programming languages, with support for many other languages.[110] The default firmware is closed source, while an unofficial open source is available.

# Raspberry Pi and Internet of Things

[check out the introduction documents](https://projects.raspberrypi.org/en/projects/raspberry-pi-getting-started)
[79 raspberry pi projects](https://pimylifeup.com/category/projects/)

# Using the Terminal (Command Line)

All computers have a terminal (in windows its called command prompt)
Mac - ``` "/Applications/Utilities"```
Windows - ```"C:\Windows\system32\cmd.exe"``` alternativley just search 'command prompt' from the start menu

once you have it open try this simple command -

``` $ say hello world```

# Connecting to the Raspberry Pi from your computer

how to find our pi's Ip address (note you need to be on the same wifi network*)
choices =
``` $ ping raspberrypi.local```

Getting the IP address of a Pi using your smartphone
The Fing app is a free network scanner for smartphones. It is available for [Android](https://play.google.com/store/apps/details?id=com.overlook.android.fing) and [iOS](https://itunes.apple.com/gb/app/fing-network-scanner/id430921107?mt=8)

Your phone and your Raspberry Pi have to be on the same network, so connect your phone to the correct wireless network.

When you open the Fing app, touch the refresh button in the upper right-hand corner of the screen. After a few seconds you will get a list with all the devices connected to your network. Scroll down to the entry with the manufacturer "Raspberry Pi". You will see the IP address in the bottom left-hand corner, and the MAC address in the bottom right-hand corner of the entry.

# Remote Login to Raspberry Pi
SSH
(secure Shell)
Secure Shell (SSH) is a cryptographic network protocol for operating network services securely over an unsecured network.[1] Typical applications include remote command-line login and remote command execution, but any network service can be secured with SSH.
* Make a note of your RPI's IP address so you can remotely log in again.
We are going to use SSH to login remotely from your computers to your Raspberry PI computers...

![alt text](/images/terminalssh1.png)
![alt text](/images/terminalssh2.png)

![alt text](/images/terminal-commands.png)
* [Getting started with Raspberry pi GPIO](https://www.w3schools.com/nodejs/nodejs_raspberrypi_gpio_intro.asp)

# Raspberry Pi and Internet of Things

* [check out the introduction documents](https://projects.raspberrypi.org/en/projects/raspberry-pi-getting-started)
* [79 raspberry pi projects](https://pimylifeup.com/category/projects/)
* [Getting started with Raspberry pi GPIO](https://www.w3schools.com/nodejs/nodejs_raspberrypi_gpio_intro.asp)
