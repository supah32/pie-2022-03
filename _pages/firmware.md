---
title: "Firmware Design"
permalink: /firmware/
---

<a href="https://github.com/ayushchakra/autonomous-robot-vacuum" target="_blank" style="float: right; text-decoration: none; font-size: 20px; color: #000000; background-color: #cbcbcb; border: none; border-radius: 10px; padding: 10px; padding-right: 20px; padding-left: 20px;">
	View on GitHub
</a>

<h1 style="display: inline-block; margin-right: auto;">Firmware Design</h1>


The firmware consisted of the DC motor controls and the fan power. Because the robot utilized four mecanum wheels, there needed to be four motors. We interfaced between our Arduino and the DC motors with <a href="https://www.adafruit.com/product/1438" target="_blank">Adafruit’s motor shield</a>, which came with a free <a href="https://learn.adafruit.com/adafruit-motor-shield/library-install" target="_blank">motor control library for Arduino</a>. Using the library's commands, we wrote custom functions to change the speeds and directions of the four motors so the the robot could move in 8 directions (and also rotate). Motor speeds were set using the library's `setSpeed()` function, and then directions were determined using `run()`. As an example, here is a function to drive the robot left.

```
void driveWest(){
  frontRightMotor->setSpeed(50);
  frontLeftMotor->setSpeed(50);
  backLeftMotor->setSpeed(50);
  backRightMotor->setSpeed(50);
  
  frontRightMotor->run(FORWARD);
  frontLeftMotor->run(BACKWARD);
  backLeftMotor->run(FORWARD);
  backRightMotor->run(BACKWARD);
}
```

The four wheels needed to turn in specific and independent directions in order for the robot to achieve movement in certain directions. For example, to move left, the front right and back left wheels move forward while the front left and back right move backwards. Below is a diagram depicting all of this.

<img src="/assets/images/wheel_directions.jpg" alt="Individual wheel directions for moving in specific directions" style="
	display: block;
	margin-right: auto;
	margin-left: auto;
	width: 70%;
	"
/>

<br>

Other than the DC motors, the vacuum fan was also controlled by the Arduino using PWM. Because we just wanted the fan to run continuously without changing speed or direction, we just had to repeatedly send the same signal to the fan.

