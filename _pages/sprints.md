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

<img src="{{ site.baseurl }}/assets/images/sprint_1_car.jpg" alt="Image of assembled MVP car" style="display: block;
	margin-left: auto;
	margin-right: auto;
	width: 40%;"
/>

During this time, we also ideated on the integration of components. This was more crucial to the development of the vacuum mechanism and how it would integrate with other important pieces like the LiDAR.

<img src="{{ site.baseurl }}/assets/images/chassis_diagram.png" alt="Hand-drawn diagram of the final chassis plan" style="display: block;
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

<img src="{{ site.baseurl }}/assets/images/sprint_2_car.png" alt="Image of the assembled robot for the sprint 2 demo" style="display: block;
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

<img src="{{ site.baseurl }}/assets/images/fan.png" alt="Image of the fan used to vacuum" style="display: block;
	margin-left: auto;
	margin-right: auto;
	width: 35%;"
/>

At this point, we built the vacuuming mechanism with a fan that did not have powerful enough airflow to uptake some items. With simple testing, however, we found the mechanism to work and would work more efficiently with a more powerful fan attached. 

<img src="{{ site.baseurl }}/assets/images/final_chassis.jpg" alt="Ayush and a hastily-assembled version of the final vehicle design" style="display: block;
	margin-left: auto;
	margin-right: auto;
	width: 40%;"
/>


## Technical Challenges (Stepper Motors)

The biggest challenge we faced throughout the process of creating the final design was working with the stepper motors. In our original design, we used 6V Nema 8 stepper motors. Although we successfully got them working, we experienced a lot of issues with the motors overheating if they were powered for more than a few minutes (which melted the 3D-printed wheel adapters). Furthermore, the motors were so small that they buckled under the weight of all the chassis/electronics components.

In Sprint 3, we attempted to remedy these issues by using <a href="https://www.amazon.com/Stepper-Motor-Bipolar-64oz-Printer/dp/B00PNEQI7W" target="_blank">12V Nema 17 stepper motors</a>. Since these ran on 12V instead of 6V, it prevented the overheating issue. However, when trying to use them, the entire motor system would stutter/freeze up. Because of this, debugging was difficult as we couldn't easily pinpoint what component had failed. We had to check all the wirings and the software each time this occurred, which was a huge time sink. We discovered that one of the (<a href="https://www.amazon.com/Qunqi-Controller-Module-Stepper-Arduino/dp/B014KMHSW6" target="_blank">L298N motor controllers</a>) completely stopped working.

By this time, it was too late to purchase new controllers, so we decided to cut our losses and pivot to using DC motors we had lying around. We realized that the Raspberry Pi's GPIO pins were relatively unstable (likely another contributer to the motor stuttering issue), so we started controlling the motors with an Arduino. Because of this, we also replaced our motor controllers with <a href="https://www.adafruit.com/product/1438" target="_blank">Adafruit’s Arduino motor shield</a>, which could drive all 4 DC motors.


<br>
<br>


## Gallery

<div>
	<div>
		<img src="{{ site.baseurl }}/assets/images/iso_view_1.png" alt="Isometric view of the robot" style="display: inline-block;
			width: 30%;"
		/>
		<div style="display: inline-block; width: 3%"></div>
		<img src="{{ site.baseurl }}/assets/images/iso_view_2.png" alt="Isometric view of the robot" style="display: inline-block;
			width: 30%;"
		/>
		<div style="display: inline-block; width: 3%"></div>
		<img src="{{ site.baseurl }}/assets/images/front_view.png" alt="Isometric view of the robot" style="display: inline-block;
			width: 30%;"
		/>
	</div>

	<div style="height: 5%"></div>

	<div>
		<img src="{{ site.baseurl }}/assets/images/side_view_1.png" alt="Isometric view of the robot" style="display: inline-block;
			width: 30%;"
		/>
		<div style="display: inline-block; width: 3%"></div>
		<img src="{{ site.baseurl }}/assets/images/side_view_2.png" alt="Isometric view of the robot" style="display: inline-block;
			width: 30%;"
		/>
		<div style="display: inline-block; width: 3%"></div>
		<div style="display: inline-block; width: 30%"></div>
	</div>
</div>