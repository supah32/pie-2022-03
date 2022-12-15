---
title: "Sprints"
permalink: /sprints/
sidebar:
  nav: docs
---


# Sprint Timeline Breakdown

We were given 6 weeks to iterate and complete the final design, which we divided into three 2-week sprints.


## Sprint 1: MVP

**Goals:**
* Assemble simple vehicle with DC motors and mecanum wheels
* Create keyboard controls for vehicle movement in 8 directions using Arduino

**Purpose:** Test movement and physics of mecanum wheels.

<img src="/assets/images/sprint_1_car.jpg" alt="Image of assembled MVP car" style="display: block;
	margin-left: auto;
	margin-right: auto;
	width: 40%;"
/>

During this time, we also ideated on the integration of components. This was more crucial to the development of the vacuum mechanism and how it would integrate with other important pieces like the LiDAR.

<img src="/assets/images/chassis_diagram.png" alt="Hand-drawn diagram of the final chassis plan" style="display: block;
	margin-left: auto;
	margin-right: auto;
	width: 50%;"
/>




## Sprint 2

**Goals:**
* Get stepper motors working
* Replace Arduino with Raspberry Pi
* Parse LiDAR data
* Create custom chassis to mount all parts

**Purpose:** Get LiDAR working on its own, replace MVP components with more advanced options.

<img src="/assets/images/sprint_2_car.png" alt="Image of the assembled robot for the sprint 2 demo" style="display: block;
	margin-left: auto;
	margin-right: auto;
	width: 40%;"
/>

During the preparation for this sprint, we encountered many problems involving the wheels and the motors. The stepper motors we used produced enough heat to melt the 3D printed couplers needed to attach the motors to the mecanum wheels. Due to this inconvenience, the set up for the LiDAR was completed separately and dismounted from the chassis.

We would also like to note, this is where we forgot about the orientation of the mecanum wheels. This caused further problems with the movement of the robot, which added onto our problems immensely for this sprint deliverable.  



## Sprint 3

**Goals:**
* Implement new (larger) stepper motors and mecanum wheels
* Integrate and test LiDAR-based navigation 
* Integrate more robust navigation algorithm
* Fix cable management
* Figure out how to improve torque/ability to drive heavy chassis
* Decide upon a vacuuming method, build it

**Purpose:** finish project

<img src="/assets/images/fan.png" alt="Image of the fan used to vacuum" style="display: block;
	margin-left: auto;
	margin-right: auto;
	width: 35%;"
/>

At this point, we built the vacuuming mechanism with a fan that did not have powerful enough airflow to uptake some items. With simple testing, however, we found the mechanism to work and would work more efficiently with a more powerful fan attached. 

<img src="/assets/images/final_chassis.jpg" alt="Ayush and a hastily-assembled version of the final vehicle design" style="display: block;
	margin-left: auto;
	margin-right: auto;
	width: 40%;"
/>


## Technical Challenges:
Stepper motor controllers

Due to these challenges, we switched back from stepper motors into using DC motors. 


<br>
<br>


<div>
	<div>
		<img src="/assets/images/iso_view_1.png" alt="Isometric view of the robot" style="display: inline-block;
			width: 30%;"
		/>
		<div style="display: inline-block; width: 3%"></div>
		<img src="/assets/images/iso_view_2.png" alt="Isometric view of the robot" style="display: inline-block;
			width: 30%;"
		/>
		<div style="display: inline-block; width: 3%"></div>
		<img src="/assets/images/front_view.png" alt="Isometric view of the robot" style="display: inline-block;
			width: 30%;"
		/>
	</div>

	<div style="height: 5%"></div>

	<div>
		<img src="/assets/images/side_view_1.png" alt="Isometric view of the robot" style="display: inline-block;
			width: 30%;"
		/>
		<div style="display: inline-block; width: 3%"></div>
		<img src="/assets/images/side_view_2.png" alt="Isometric view of the robot" style="display: inline-block;
			width: 30%;"
		/>
		<div style="display: inline-block; width: 3%"></div>
		<div style="display: inline-block; width: 30%"></div>
	</div>
</div>


