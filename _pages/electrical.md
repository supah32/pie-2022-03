---
title: "Electrical Design"
permalink: /electrical/
sidebar:
  nav: design
---

The electrical circuit consisted of an Arduino (with motor shield), a Raspberry Pi, 4 DC motors, a battery, a RPLiDAR, and a fan for the vacuum. The wiring diagram is in the image below.

<img src="/assets/images/hardware_diagram.png" alt="A hardware diagram showing connections between electrical components" style="
	display: block;
	"
/>


### Raspberry Pi

<img src="/assets/images/rasp_pi.png" alt="Image of the Raspberry Pi 4b" style="
	/*display: inline-block;*/
	width: 30%;
	float: right;
	"
/>
<div style="display: inline-block;
	width: 65%;">
	A 1 GB Raspberry Pi 4b was used as the main processor on the car. It was powered by a USB-C connector that is attached to a 12V-5V buck converter. Additionally, the USB ports of the Raspberry Pi are being used to power and communicate with the Arduino and the LiDAR.
</div>


<br>


### Arduino

<img src="/assets/images/arduino_uno.png" alt="Image of the Arduino Uno" style="
	/*display: inline-block;*/
	width: 30%;
	float: right;
	"
/>
<div style="display: inline-block;
	width: 65%;">
	An Arduino Uno was used to control the DC motors. It provided simplicity in writing controls, and also interfaced easily with the motor shield we had on hand. Additionally, the Arduino provided an interface to provide 12V DC power to the motor shield from the battery.
</div>


<br>


### DC Motors and Shield

The robot utilized 4 DC motors, which we acquired through the '<a href="https://www.amazon.com/Mecanum-Wheel-Chassis-Aluminum-Education/dp/B09CPZ51N4/ref=sr_1_11?keywords=mecanum+wheel+robot+car+chassis&qid=1670878668&sprefix=mecanum+wheel%2Caps%2C73&sr=8-11" target="_blank">Mecanum Wheel Chassis Car</a>' kit. These were controlled using <a href="https://www.adafruit.com/product/1438" target="_blank">Adafruit’s Arduino motor shield</a>, which allowed for easy, decoupled control over the motor’s speeds and directions. The shield directly interfaced with the Arduino Uno.

<div style="
	margin-left: auto;
	margin-right: auto;
">
<img src="/assets/images/dc_motor.jpg" alt="Image of the DC motor" style="display: inline-block;
	width: 25%;
	margin-right: 10%;
	"
/>
<img src="/assets/images/motor_shield.jpg" alt="Image of the motor shield" style="display: inline-block;
	width: 50%;
	margin-left: 10%;
	"
/>
</div>


<br>


### Battery + Buck Converter

We chose to use a <a href="https://www.amazon.com/dp/B06XKNM73N?psc=1&ref=ppx_yo2ov_dt_b_product_details" target="_blank">14.8V, 3Ah battery</a>. All components were in parallel, so to choose the voltage specifications we just needed to figure out what the highest required voltage was (12V, for the motor shield). We also needed a current specification, since the total current draw of the circuit was the sum of all the parallel components.

Beyond the motor shield, the Raspberry Pi was directly powered through the battery. The Raspberry Pi requires 5V, so we implemented a <a href="https://www.amazon.com/dp/B07Y2V1F8V?psc=1&ref=ppx_yo2ov_dt_b_product_details" target="_blank">buck converter</a> that allowed us to step down from the battery’s 12V to 5V.


<img src="/assets/images/battery.png" alt="Image of the battery" style="display: inline-block;
	width: 50%;
	margin-right: 4%;
	margin-left: 4%;
	"
/>
<img src="/assets/images/buck_converter.png" alt="Image of the buck converter" style="display: inline-block;
	width: 30%;
	margin-right: 4%;
	margin-left: 4%;
	"
/>


All other components were powered through either the Raspberry Pi or the motor shield. For example, the 4 DC motors received power through the motor shield, not directly through the battery.


<br>


<img src="/assets/images/lidar.png" alt="Image of the RPLiDAR" style="
	/*display: inline-block;*/
	width: 30%;
	float: right;
	"
/>

### LiDAR scanner

<div style="display: inline-block;
	width: 65%;">
	The scanner we used was the <a href="https://www.slamtec.com/en/Lidar/A1" target="_blank">RPLIDAR A1M8</a>. We powered the LiDAR with a USB, which allowed us to provide a stable 5V power supply and communicate with the device over serial.
</div>


<br>


### Vacuum fan

One of the main features of the autonomous robot was that it could vacuum. For this, we constructed our own vacuuming system using a <a href="https://www.amazon.com/dp/B07SGWNV5J?ref=ppx_yo2ov_dt_b_product_details&th=1" target="_blank">powerful PC cooling fan</a>, a box for debris storage, a dust filter, and PVC pipes. This design was inspired by existing homemade vacuum designs such as <a href="https://www.youtube.com/watch?v=2bAAlp3Dyvc" target="_blank">this one</a>.

[diagram of vacuum system here]

The vacuum system was mounted so that the PVC tube (through which debris on the ground would be sucked through) was directly in the center of the robot, and the debris storage box was attached upright on the back of the chassis. Because the box was so tall, the LiDAR had to be mounted on standoffs so that its perception would not be obstructed.

[image of vacuum on chassis here]

