---
title: "Electrical Design"
permalink: /electrical/
---

# Electrical System Design

<!-- A detailed description of electrical design (circuit diagrams are appropriate) and any necessary analysis -->

The electrical circuit consisted of an Arduino (with motor shield), a Raspberry Pi, 4 DC motors, a battery, a RPLiDAR, and a fan for the vacuum.

#### Raspberry Pi

A 1 GB Raspberry Pi 4b was used as the main processor on the car. It was powered by a USB-C connector that is attached to a 12V-5V buck converter. Additionally, the USB ports of the Raspberry Pi are being used to power and communicate with the Arduino and the LiDAR.

#### Arduino

An Arduino Uno was used to control the DC motors. It provided simplicity in writing controls, and also interfaced easily with the motor shield we had on hand. Additionally, the arduino provided an interface to provide 12V DC power to the motor shield from the battery.

#### DC Motors and Shield

The robot utilized 4 DC motors, which we acquired through the [https://www.amazon.com/Mecanum-Wheel-Chassis-Aluminum-Education/dp/B09CPZ51N4/ref=sr_1_11?keywords=mecanum+wheel+robot+car+chassis&qid=1670878668&sprefix=mecanum+wheel%2Caps%2C73&sr=8-11](‘Mecanum Wheel Chassis Car’) kit. These were controlled using [https://www.adafruit.com/product/1438](Adafruit’s Arduino motor shield), which allowed for easy, decoupled control over the motor’s speeds and directions. The shield directly interfaced with the Arduino Uno.

#### Battery + Buck Converter

We chose to use a [https://www.amazon.com/dp/B06XKNM73N?psc=1&ref=ppx_yo2ov_dt_b_product_details](14.8V, 3Ah battery). All components were in parallel, so to choose the voltage specifications we just needed to figure out what the highest required voltage was (12V, for the motor shield). We also needed a current specification, since the total current draw of the circuit was the sum of all the parallel components.

Beyond the motor shield, the Raspberry Pi was directly powered through the battery. The raspberry pi requires 5V, so we implemented a buck converter that allowed us to step down from the battery’s 12V to 5V.

All other components were powered through either the Raspberry Pi or the motor shield. For example, the 4 DC motors received power through the motor shield, not directly through the battery.

#### LiDAR scanner

The scanner we used was the [https://www.slamtec.com/en/Lidar/A1](RPLIDAR A1M8). We powered the LiDAR with a USB, which allowed us to provide a stable 5V power supply and communicate with the device over serial.

#### Vacuum fan
