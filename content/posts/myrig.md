+++
title = "My Rig"
date = "2023-08-30T01:03:18-04:00"
author = "David Farje"
authorTwitter = "" #do not include @
cover = ""
tags = ["rig", "lab"]
keywords = ["rig", "amd", "ryzen"]
description = "introduction to my rig is my development enviroment"
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++

## Introduction

I thought I would give a brief overview of my development/learning environment.  Many of my wacky experiments are going to be done on a rig I built in 2022. In 2022, I was working as a cybersec consultant and decided to build a rig that would help me with what I was working on at the time.  Mostly, I was going to be running many simultaneous VMs in complex topologies and running DDoS mitigation experiments on them.  I required a lot of memory and decent CPU.


## The Hardware

I ordered the parts from many different places I will not be posting the BOM here I will be posting the inxi output of the machine.  The experiments done here can be done on any machine.

```shell

symtex@hypervisor:~$ sudo inxi -b
System:    Host: hypervisor.seclinux.net Kernel: 5.15.0-79-generic x86_64 bits: 64 Console: tty 1 
           Distro: Ubuntu 20.04.6 LTS (Focal Fossa) 
Machine:   Type: Desktop Mobo: ASUSTeK model: TUF GAMING X570-PLUS (WI-FI) v: Rev X.0x serial: xxxxxxxxxxxxxxx 
           BIOS: American Megatrends v: 4204 date: 02/25/2022 
CPU:       16-Core: AMD Ryzen 9 5950X type: MT MCP speed: 2199 MHz min/max: 2200/3400 MHz 
Graphics:  Device-1: NVIDIA GK208B [GeForce GT 730] driver: nvidia v: 470.199.02 
           Display: server: X.org 1.20.13 driver: nvidia unloaded: fbdev,modesetting,nouveau,vesa tty: 140x34 
           Message: Advanced graphics data unavailable in console for root. 
Network:   Device-1: Intel Wireless-AC 9260 driver: iwlwifi 
           Device-2: Realtek RTL8111/8168/8411 PCI Express Gigabit Ethernet driver: r8169 
Drives:    Local Storage: total: 2.27 TiB used: 223.63 GiB (9.6%) 
Info:      Processes: 428 Uptime: 1h 43m Memory: 125.70 GiB used: 1.04 GiB (0.8%) Init: systemd runlevel: 5 Shell: bash 
           inxi: 3.0.38 

```

## The software

I decided not to use the latest LTS but one that's a bit older (Focal Fossa).  I do this for stability reasons and availability of documentation.  In the past, I've used Debian as the distro of choice for my home servers or rigs but this time I wanted to use Ubuntu mate.  Ubuntu mate first became my favorite distro via laptop use, then I eventually ended up using it on my home servers/rigs.  At work it's a all Red Hat and so this blog will obviously contain Red Hat content.

## KVM, libvirt, and OVS

When it comes to spinning up the necessary environments I like to use Vanilla KVM/libvirt with OpenVSwitch.  I know there are higher level abstraction tools like eve-ng, gns3, etc etc.  I prefer this setup because I feel I have manual control of all aspects of configuration this helps me at time of debugging.

