---
title: "Zoomba"
permalink: /
---


*An autonomous, omnidirectional, vacuuming robot.*


The Zoomba is a speedy, efficiently-navigating cleaning robot. Unlike most cleaning robots, the Zoomba includes mecanum wheels to manuever through rooms and obstacles omnidirectionally. The Zoomba is able to pick up light pieces of trash from the floor and dust particles when moving around the room.


## Final System

<img src="{{ site.baseurl }}/assets/images/iso_render.jpg" alt="CAD assembly of the entire chassis and all components" style="display: block;
	margin-left: auto;
	margin-right: auto;"
/>


### Mechanical

The mechanical side focused on designing a chassis and mounting solutions to hold all hardware components. Additionally, part fo the mechanical design involved a custom vacuuming system.

[Read more about our mechanical design and fabrication.](mechanical.md)

### Electrical

The electrical components revolved around the LiDAR and motors. Microcontrollers were used to parse data and send commands, and power supplies were managed to provide ample voltage and current to all components.

[Read more about our power supply management and microcontroller usage.](electrical.md)

### Firmware

The firmware consisted of motor and vacuum controls.

[Read more.](firmware.md)

### Software

The software supports two robot behaviors: remote control and autonomous navigation. With remote control, a user can use a laptop keyboard to control the robot's motion. With autonomous navigation, the robot's direction is calculated based on obstacel data gathered from the LiDAR.

[Read more about ROS nodes, obstacle avoidance, and Raspberry Pi/Arduino communications.](software.md)

## Timeline

We were given 7 weeks to create the Zoomba. We broke this down into three 2-week sprints, with an extra week at the end to finalize everything. These sprints were structured using the SCRUM agile framework.

[Read more about our sprint breakdown and what we accomplished.](sprints.md)

