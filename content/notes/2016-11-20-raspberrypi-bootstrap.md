---
title: "🇬🇧 Raspberrypi bootstrap"
subtitle: ""
date: 2016-11-20
draft: false
---

## Installation

### Download the image

https://www.raspberrypi.org/downloads/

### Install the image on your SD card

#### List the disk

    diskutil list

Identify the disk (not partition) of your SD card e.g. `disk4`, not `disk4s1`

#### Unmount your SD card by using the disk identifier

    diskutil unmountDisk /dev/disk<disk# from diskutil>

#### Copy the data to your SD card

    sudo dd bs=1m if=image.img of=/dev/rdisk<disk# from diskutil>

You can check the progress by sending a `SIGINFO` signal (press `Ctrl+T`).

## SSH

### Get the IP adress of the Raspberry PI

#### Scan your sub network

    ifconfig
    nmap -sn 192.168.1.0/24
    ssh pi@192.168.1.53

* login : pi
* password : raspberry

### Passwordless ssh access

#### Check for existing ssh keys

    ls ~/.ssh

#### Generate new ssh keys on your machine

    ssh-keygen -t rsa -C username@pi

#### Copy your public key to your raspberry pi

    cat ~/.ssh/id_rsa.pub | ssh pi@192.168.1.53 'cat >> .ssh/authorized_keys'

## VNC Server

### Install Real VNC

    brew cask install real-vnc

### Launch server

    sudo raspi-config
    vncserver :1

* host : 192.168.1.53:1
* username : pi
* password : raspberr

#### Start server auto at boot

    cd /home/pi
    cd .config
    mkdir autostart
    cd autostart
    sudo vi tightvnc.desktop

```sh
#!/bin/sh
[Desktop Entry]
Type=Application
Name=tightVNC
Exec=vncserver :1
StartupNotify=false
```

    sudo reboot