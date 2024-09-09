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

### (Optional but Recommended) Set a Static IP

This is a convenience change that will make it easier to find and connect to your camera later.  There is an [exhaustive page](https://www.raspberrypi.org/documentation/configuration/tcpip/) provided by the Raspberry Pi Foundation, but an example has been included below.  Note that if you are using SSH to connect to your RPi, you will need to reconnect to the new IP once you have changed it.

__WiFi Networking Example__

Modify the file <b>/etc/dhcpcd.conf</b> to read as follows:
```sh
interface wlan0
static ip_address=192.168.1.45/24    
static routers=192.168.1.1
static domain_name_servers=208.67.220.220 8.8.8.8
```
*For a wired network connection, change the interface from "wlan0" to the appropriate "eth" interface as found in 'ip address | grep eth'
*You will need to ensure your IP address, router, and domain name servers are appropriate for your network

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

Follow the steps below to update the software your Pi runs (may take a minute):
```sh
sudo apt-get update
sudo apt-get upgrade
```


