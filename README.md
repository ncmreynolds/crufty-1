# Crufty 1

## Introduction

Crufty is a 'robot' rover made from 'maker cruft'; those things likely to be filling the drawers/storage boxes/garages/cellars/Hackspaces of people who make stuff with small board computers, microcontrollers and 3D printers. Crufty deliberately uses older versions/tech so lower performance/outdated hardware can be repurposed.

The hardest part to source will be hoverboards with the same controllers used in this build, it's a bit of a pot luck what is fitted. If the project is successful I may try and document builds for other common hoverboard controllers.

The intention is that Crufty can be made for a comparatively small outlay and used as a 'learning platform' for Robot OS (ROS) without purchasing large amounts of expensive stuff. Crufty is much bigger than a typical tabletop/indoor robot made with small DC brushed motors but scales many of the usual ideas up so Crufty can be used outdoors (although sunlight stops the Kinect working).

This repository is a rough how-to/log of building Crufty so I can collect hard to find information in one place.

### Tools/facilities/skills needed

- Very basic woodworking/fabrication
- Soldering
- 3D printing (mostly for ease, you could fabricate everything needed with basic tools)
- Basic experience with Arduino coding (on any platform, but examples will be created on Windows 10)
- Basic experience with Linux (for the Raspberry Pi/ROS)
- A computer that can run ROS (any platform, but examples will be on Ubuntu 20.04 LTS)
- ST-Link v2 for flashing the Hoverboard controllers

### High level BOM (TBC)

- Two self balancing hoverboards (with Gen 2 controllers specifically supported by the hack firmware)
- Raspberry Pi 2/3/4 & 8GB SD card (or larger)
- Microsoft Kinect 360 (smaller point cloud, more manageable than Kinect One)
- Arduino Nano (or other AVR microcontroller you may have)
- HC-SR04 ultrasonic range finders x 3-8
- Generic USB GPS module
- Wemos D1 mini (or other ESP8266 dev board) x 2
- Wii Nunchuck controller

### High level software manifest (TBC)

- Ubuntu 20.04 LTS on Raspberry Pi (to keep Pi 2/3 usable)
- [Robot OS](https://www.ros.org/) 1 LTS Noetic Ninjemys
- [Arduino IDE](https://www.arduino.cc/en/software) 1.8.x (to build code for the ESP/Arduinos)
- [Open Kinect](https://openkinect.org/wiki/Main_Page) (for Kinect 360 support)
- Gen 2 hoverboard hack firmware, specifically [this fork](https://github.com/pieterjanbuntinx/Hoverboard-Firmware-Hack-Gen2) by Pieter-Jan Buntinx
- [OpenSCAD](https://openscad.org/) was used for designing the 3D printed parts and the source files are provided

## Getting started

First have a root around and see which of the parts you can find, price up the likely cost of what you don't and decide if you've got the time and budget to build a Crufty. Even with a lot of *very* basic parts needed a rover this size can get quite expensive.

The build is documented in a number of sections, all of which can be built kind of independently, but you should start with the chassis and attach things as you go.

## Sections

### Chassis

### Hoverboard controllers

### Hoverboard motors

### Kinect 360

### Nunchuck controller

### Raspberry Pi

### Ultrasonic array