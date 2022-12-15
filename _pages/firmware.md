---
title: "Firmware Design"
permalink: /firmware/
---

# Firmware Design

[https://github.com/ayushchakra/autonomous-robot-vacuum/tree/main/final_demo/arduino_interface](https://github.com/ayushchakra/autonomous-robot-vacuum/tree/main/final_demo/arduino_interface)

The firmware encapsulated the DC motor controls. The robot's mecanum wheel-dependent design called for four motors. To control the motors, we used [https://learn.adafruit.com/adafruit-motor-shield/library-install](Adafruit’s motor library), which directly worked with the motor shield. Using the library’s commands, we wrote custom functions to change the directions and speeds of the four motors, allowing the robot to move in 8 directions and rotate. We also use PWM to send commands to our fan from Arduino.

