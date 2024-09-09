# rpi_pantilt

## What Is This Repo For?
This repo supports the creation of an automatic pan/tilt camera that can follow a human (or other selected entity).  The repo assumes the use of a Raspberry Pi platform and requires a Coral TPU for best performance (see hardware requirements for more details).

## Acknowledgements
This work is based __heavily__ on a post by Leigh Johnson in Towards Data Science.


## Hardware Requirements

### Hardware Platform 1.0 (RPi 4)
Big Stuff:
- Raspberry Pi 4 (4GB)
- Argon NEO Case for Raspberry Pi 4 (fits nicely with the lid off)
- Raspberry Pi Camera v2
- 12" CSI/DSI Ribbon Cable for Raspberry Pi Camera (you'll want this!)
- Pimoroni Pan-Tilt Hat Kit
- Coral Edge TPU (USB)

Little Stuff:
- 128GB MicroSD Card (overkill; 32GB probably fine)
- Micro HDMI to HDMI (M to F) adapter
- Power supply for the Raspberry Pi

### Future Hardware to Test
Items I would like to test against this guide to see if we can realize performance gains:
- Raspberry Pi 5 (8GB)
- Raspberry Pi Camera v3
- Raspberry Pi 5 AI Kit (13 TOPS), OR;
- Coral M.2 Accelerator with Dual Edge TPU (needs RPi M.2 hat) (8 TOPS)
- RGB NeoPixel Stick (Adafruit product: 8x 5050 RGB LED with integrated drivers)


## Hardware Setup and Bootstrapping

### Initial Raspberry Pi Setup
For initial setup, see this repo: [RPi Setup](https://github.com/mrccie/rpi_setup)


### (Optional) Install VIM (because it's best!)

Follow the steps below to install the VIM text editor:
```sh
sudo apt-get install -y vim
```

### (Optional) Set a Static IP

This is a convenience change that will make it easier to find and connect to your camera later.  The recommended approach is to create a static reservation on your DHCP server, however if that is not possible or not desired then follow these steps.

There is an [exhaustive page](https://www.raspberrypi.org/documentation/configuration/tcpip/) provided by the Raspberry Pi Foundation, but an example has been included below.  Note that if you are using SSH to connect to your RPi, you will need to reconnect to the new IP once you have changed it.

__WiFi Networking Example__

Identify the interface to update with the command:
```sh
sudo nmcli con show
```

In my case, I preconfigured the WiFi interface and it is listed as "preconfigured".  So I proceed as follows to set a static IP, DNS servers, and restart the interface:
```sh
sudo nmcli con mod preconfigured ipv4.addresses 192.168.1.45/24 ipv4.method manual
sudo nmcli con mod preconfigured ipv4.gateway 192.168.1.1
sudo nmcli con mod preconfigured ipv4.dns "208.67.220.220 8.8.8.8"
sudo nmcli con down preconfigured && sudo nmcli c up preconfigured
```
*You will need to ensure your IP address, router, and domain name servers are appropriate for your network
*It took a minute or two after the last command for the WiFi to come back up; please be patient

### (Optional but Recommended) Set your Local Timezone

Follow the steps below to set your timezone:
```sh
sudo raspi-config
> 5 - Localization Options
>> L2 - Timezone
>>> Pick accordingly
>>>> Finish
```

### (Optional but Strongly Recommended) Update the Operating System

Follow the steps below to update the software your Pi runs (expect this to take awhile):
```sh
sudo apt-get update
sudo apt-get upgrade
```


