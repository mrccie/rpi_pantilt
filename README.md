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


## Raspberry Pi Setup
