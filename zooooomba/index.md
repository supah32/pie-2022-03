---
title: Zoomba
subtitle: An autonomous, omnidirectional, vacuuming robot
layout: page
callouts: home_callouts
show_sidebar: false
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

<!-- TODO: change this into a button -->
view info here


## Firmware Design

View more here

## Software Design

View more here


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
