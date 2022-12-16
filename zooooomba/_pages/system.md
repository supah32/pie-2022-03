---
title: "System Design"
permalink: /system/
sidebar:
  nav: design
---

The robot can be driven in two different ways, each with its own accompanying system.

To navigate autonomously, the robot uses obstacle detection via the LiDAR to determine the path of "least resistance". The direction of "least resistance" is then converted to a drive direction command, and sent to the Arduino via serial. The Arduino is then able to command the directions and speeds of the four wheels to drive in the correct direction.

<img src="{{ site.baseurl }}/assets/images/power_dist.png" alt="Flow diagram of autonomous driving system" style="
  display: block;
  "
/>

A second system is TeleOp-based: a user can provide keyboard inputs on a laptop to manually change the direction of the car. With ROS, the key input is sent to the Raspberry Pi, parsed into a drive direction, and forwarded to the Arduino through a serial connection. And similar to the autonomous system, the Arduino determines wheel directions and speeds to drive in the specified direction. TeleOp was used in our MVP and also during development to override driving-related bugs in the code.

<img src="{{ site.baseurl }}/assets/images/teleop_diagram.png" alt="Flow diagram of tele-op controls" style="
  display: block;
  "
/>

Parallel to both of these systems is the vacuuming system, which runs a computer fan at an unchanging speed. It is controlled continuously through PWM, and collects debris on the ground.


