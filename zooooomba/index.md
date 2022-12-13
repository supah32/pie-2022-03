---
title: Zoomba
subtitle: An autonomous, omnidirectional, vacuuming robot
layout: page
callouts: home_callouts
show_sidebar: true
---

## Objectives

The Zoomba is a speedy, efficiently-navigating cleaning robot. <Idk idk idk something inspiring here about it>


## Final System


## System Diagram


## Mechanical Design

#### Chassis

#### Mecanum Wheels

#### Vacuum



## Electrical Design

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


## Firmware Design

[https://github.com/ayushchakra/autonomous-robot-vacuum/tree/main/final_demo/arduino_interface](https://github.com/ayushchakra/autonomous-robot-vacuum/tree/main/final_demo/arduino_interface)

The firmware encapsulated the DC motor controls. The robot's mecanum wheel-dependent design called for four motors. To control the motors, we used [https://learn.adafruit.com/adafruit-motor-shield/library-install](Adafruit’s motor library), which directly worked with the motor shield. Using the library’s commands, we wrote custom functions to change the directions and speeds of the four motors, allowing the robot to move in 8 directions and rotate. We also use PWM to send commands to our fan from Arduino.

## Software Design

[https://github.com/ayushchakra/autonomous-robot-vacuum/tree/main/final_demo/robot_vacuum](https://github.com/ayushchakra/autonomous-robot-vacuum/tree/main/final_demo/robot_vacuum)

The final software architecture is split into two main behaviors: remote control and autonomous navigation. Each behavior is encapsulated into separate ROS Nodes, allowing for quick toggling between behaviors simply based on the Node being run on the necessary devices. This also allows flexibility for users to suit their individual needs on a case-by-case basis. Below, you will find a more detailed explanation of each major software component.

#### Software Dependencies:

* [https://pyserial.readthedocs.io/en/latest/](pySerial)
* [https://docs.ros.org/en/foxy/Installation.html](ROS2 Foxy)
* [https://github.com/SkoltechRobotics/rplidar](rplidar)
* Keyboard Input (tty, sys, select, termios)

#### Arduino/Raspberry Pi Communications

#### LiDAR

#### ROS


## Budget Breakdown
We were given $250 to spend on materials.

| Item 									|  Cost  |
| ---- 									| ------ 	|
| L298N Controller Board (x5) 					| $37.15 |
| Raspberry Pi PSU (x1) 						| $6.36  |
| Nema Stepper Motors (x5) 					| $43.55 |
| 10A Fuses 								| $4.00  |
| 2A Fuses 								| $2.00  |
| Lipo Battery, Buck converter, USB C Cable - USB A Cable 	| $47.16 |
| Mecanum Wheel Set 						| $39.99 |
| 5V USB Fan (for vacuum) 					| $15.93 |

In addition to the purchased materials, we could use whatever materials we acquired for free. For these, we have estimated the costs.

| Item | Estimated Cost |
| ---- | ---- |
| Wires	| $5 |
| Proto Board | $5 |
| Electrical Terminals | $5 |


## Sprint Organization

We were given 6 weeks to iterate and complete the final design, which we divided into three 2-week sprints.


#### Sprint 1: MVP

**Goals:**
Assemble simple vehicle with DC motors and mecanum wheels
Create keyboard controls for vehicle movement in 8 directions using Arduino

**Purpose:** Test movement and physics of mecanum wheels.


#### Sprint 2

**Goals:**
* Get stepper motors working
* Replace Arduino with Raspberry Pi
* Parse LiDAR data
* Create custom chassis to mount all parts

**Purpose:** Get LiDAR working on its own, replace MVP components with more advanced options.


#### Sprint 3

**Goals:**
* Implement new (larger) stepper motors and mecanum wheels
* Integrate and test LiDAR-based navigation 
* Integrate more robust navigation algorithm
* Fix cable management
* Figure out how to improve torque/ability to drive heavy chassis
* Decide upon a vacuuming method, build it

**Purpose:** finish project


### Technical challenges:
Stepper motor controllers



## Meet the team


Ayush - Software
* LiDAR implementation
* ROS bringup

Jo - Mechanical
* Chassis design and mounting
* vacuum design and mounting
* wheel design and mounting

KD - Mechanical
* Chassis design and mounting
* vacuum design and mounting
* wheel design and mounting

Lily - Electrical/Firmware
* Stepper motor research, wiring, and controls
* Circuit assembly

Omar - Electrical
* Electrical wiring management
* Power supply research/implementation
