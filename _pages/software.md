---
title: "Software Design"
permalink: /software/
---

<a href="https://github.com/ayushchakra/autonomous-robot-vacuum" target="_blank" style="float: right; text-decoration: none; font-size: 20px; color: #000000; background-color: #cbcbcb; border: none; border-radius: 10px; padding: 10px; padding-right: 20px; padding-left: 20px;">
    View on GitHub
</a>

<h1 style="display: inline-block; margin-right: auto;">Software Design</h1>

The final software architecture is split into two main behaviors: remote control and autonomous navigation. Each behavior is encapsulated into separate ROS Nodes, allowing for quick toggling between behaviors simply based on the Node being run on the necessary devices. This also allows flexibility for users to suit their individual needs on a case-by-case basis. Below, you will find a more detailed explanation of the two behaviors and the major software components involved in their implementation. The full code documentation can be found in <a href="https://github.com/ayushchakra/autonomous-robot-vacuum/tree/main/final_demo/robot_vacuum" target="_blank">this repository</a>.


### Software Dependencies

Raspberry Pi:
* <a href="https://docs.ros.org/en/foxy/Installation.html" target="_blank">ROS2 Foxy</a> - Using ROS allowed us to very easily establish a network connection between different devices, quickly run multiple processes at once, and as a wrapper for our main programming logic to modularize code.
* <a href="https://pyserial.readthedocs.io/en/latest/" target="_blank">pySerial</a> - This library allowed us to quickly establish a serial connection between the Raspberry Pi and the Arduino.
* <a href="https://github.com/SkoltechRobotics/rplidar" target="_blank">rplidar</a> - This hardware abstraction library allows us to quickly interface with the RPLIDAR and decode its messages without having to worry about lower level issues that we would have encountered when trying to decode its serial input.
* <a href="https://docs.python.org/3/library/tty.html" target="_blank">tty</a>, <a href="https://docs.python.org/3/library/sys.html" target="_blank">sys</a>, <a href="https://docs.python.org/3/library/select.html" target="_blank">select</a>, <a href="https://docs.python.org/3/library/termios.html" target="_blank">termios</a> (Keyboard Input) - We also used several libraries in order to listen to a user’s keyboard input to their terminal in order to command the remote control operation.

Arduino:
* <a href="https://github.com/adafruit/Adafruit_Motor_Shield_V2_Library" target="_blank">Adafruit Motor Shield V2 Library</a> - This hardware abstraction library allows us to simply input wheel directions and velocities in order to manage the individual wheel behaviors through DC motors.

This section outlines the software components that are essential to both behaviors running as intended.


### Raspberry Pi to Arduino Communication

Due to hardware limitations of the Raspberry Pi and computing limitations of the Arduino, we chose to integrate both controllers into our system. This meant that we needed to establish a reliable communication protocol between the two devices. We chose to implement serial due to its reliability and ease of setup as compared to the alternatives (I2C, SPI, and UART). To initialize the serial connection on the Raspberry Pi, we used pyserial through the following command:

```
ser = serial.Serial(ARDUINO_PORT, SERIAL_BAUD_RATE, timeout=1)
```

Where `ARDUINO_PORT` is the path to the USB port that the Arduino is connect to, `SERIAL_BAUD_RATE` is the baud rate of the communication (9600 bits/sec), and timeout is the timeout of the connection. Then, to write to the established connection, we can simply call:

```
ser.write(self.input_keys_to_serial[msg.data])
```

On the Arduino side, we initialize the serial connection with the following command:

```
Serial.begin(9600);
```

Then, to receive messages on the Arduino, we run:

```
if (Serial.available() > 0) {
  String a = Serial.readString();
  currDriveMode = a.toInt();
}
```

Here, we first check if there is new data to receive. If there is, then we decode it as a string and cast it as an integer, since all the data are sent as `int`s encoded into `string`s. Thus, we are able to send and receive messages between the Raspberry Pi and the Arduino.


### Arduino Interface

The Arduino sketch is also the same between the two different behaviors. First, the Arduino listens to the serial line for an inputted drive direction (expressed as an integer). For example, ‘1’ means to drive forward, so if ‘1’ is received on the serial line, the `driveNorth()` function is called. The function is as follows:

```
void driveNorth(){
  //drive straight

  //set the drive speeds
  frontRightMotor->setSpeed(DRIVE_SPEED);
  frontLeftMotor->setSpeed(DRIVE_SPEED);
  backLeftMotor->setSpeed(DRIVE_SPEED);
  backRightMotor->setSpeed(DRIVE_SPEED);
  //all motors should be going forward
  frontRightMotor->run(FORWARD);
  frontLeftMotor->run(FORWARD);
  backLeftMotor->run(FORWARD);
  backRightMotor->run(FORWARD);
}
```

First, all the motors are set to the same speed using the `set_speed()` function and the direction is set to `FORWARD` using the `run()` function. The wheel speeds and directions vary based on desired drive direction. This process is continuously done to dynamically update the robot’s drive direction as the Raspberry Pi continuously determines optimal driving directions.


### Remote Control Operation:

The Remote Control behavior is split into two main scripts: <a href="https://github.com/ayushchakra/autonomous-robot-vacuum/blob/main/final_demo/robot_vacuum/robot_vacuum/rpi_interface.py" target="_blank">rpi_interface.py</a> and <a href="https://github.com/ayushchakra/autonomous-robot-vacuum/blob/main/final_demo/robot_vacuum/robot_vacuum/laptop_interface.py" target="_blank">laptop_interface.py</a>. Each of these files contain ROS Nodes that communicate with each other, allowing for the remote control behavior.


### Laptop Interface

The primary purpose of the laptop interface is to publish the current keyboard button that the user pressed. This is done by creating a ROS publisher:

```
self.publisher = self.create_publisher(String, "vel_dir", 10)
```

This publisher publishes String objects under the topic `vel_dir` and stores the most recent 10 messages that it has sent. To receive the actual key press, we implemented a `get_key()` function:

```
def get_key(self):
  """
  This is a binding function that listens for keyboard input from
  the user and returns which key is pressed.
  """
  tty.setraw(sys.stdin.fileno())
  select.select([sys.stdin], [], [], 0)
  key = sys.stdin.read(1)
  termios.tcsetattr(sys.stdin, termios.TCSADRAIN, self.settings)
  return key
```

This function sets the listener as the user’s terminal and reads it for an input for 1 second, returning the result. Once the key is received, it is published by the ROS publisher defined earlier. This process is continuously called in order to continuously stream the user’s input to the Raspberry Pi.


### Raspberry Pi Interface

The ROS Node on the Raspberry Pi serves two main purposes: subscribe to the laptop’s ROS message and send the corresponding drive direction to the Arduino. The first task is done by creating a subscriber in the node:

```
self.subscriber = self.create_subscription(
    String, "vel_dir", self.process_keyboard_input, 10
)
```

The subscriber subscribes to the String object being sent by the `vel_dir` topic and calls `self.process_keyboard_input()` (which simply stores the received key) every time a message is received. For the next task, a serial interface with the Arduino is established. Using that connection, the current key is mapped to an integer representing the desired direction and encoded into binary. This encoded value is then written to the serial bus, where the arduino receives and processes it as outlined above. This communication allows for keyboard presses from the user to be processed and sent to the Arduino to be converted into motor commands.


### Obstacle Avoidance

The Obstacle Avoidance behavior is a standalone ROS Node that commands the robot to dynamically avoid any obstacle in the robot’s environment. The full code can be found [here](https://github.com/ayushchakra/autonomous-robot-vacuum/blob/main/final_demo/robot_vacuum/robot_vacuum/obstacle_avoidance.py).


### LiDAR Analysis

In order to properly avoid obstacles we chose to implement a LiDAR to gain information about our environment. Our RPLIDAR provides a 360 degree co-planar scan centered about the LiDAR up to 15 meters in distance. Using this information, we wish to navigate the robot towards the direction of no obstacles to ensure that its motion isn’t disrupted by an obstacle. This is done by setting angle ranges for each of the 8 directions that the robot can move. Each angle range is analyzed for the number of close points (points within a certain distance threshold) and the total distance to all points within each range with the following code:

```
def process_lidar_scan(self):
    """
    After the LiDAR data is updated, it is processed to determine the number
    of close points at each cardinal direction and the total distance to
    obstacles in each direction
    """
    # Iterate through each possible direction and corresponding angle range
    for direction, angle_range in self.angle_by_dir.items():
        # Special case for south since the angle wraps around 360
        if direction == "S":
            # Find the number of points that are within the CLOSE_DIST_THRESH
            self.close_points_by_dir[direction] = len(
                [
                    point
                    for point in self.lidar_scan
                    if (point[1] > angle_range[0] or point[1] < angle_range[1])
                    and point[2] < CLOSE_DIST_THRESH
                ]
            )
            # Sum the total distance to the obstacles in the current range
            self.dist_by_dir[direction] = sum(
                [
                    point[2]
                    for point in self.lidar_scan
                    if point[1] > angle_range[0] or point[1] < angle_range[1]
                ]
            )
        else:
            # Find the number of points that are within the CLOSE_DIST_THRESH
            self.close_points_by_dir[direction] = len(
                [
                    point
                    for point in self.lidar_scan
                    if point[1] > angle_range[0]
                    and point[1] < angle_range[1]
                    and point[2] < CLOSE_DIST_THRESH
                ]
            )
            # Sum the total distance to the obstacles in the current range
            self.dist_by_dir[direction] = sum(
                [
                    point[2]
                    for point in self.lidar_scan
                    if point[1] > angle_range[0] and point[1] < angle_range[1]
                ]
            )
```

Using the two populated dictionaries, if there is a close point in all possible directions, the robot is instructed to spin in place since there is no safe distance to go. If there is a safe location to go, the direction with the least obstacles is chosen and the robot is instructed over serial to drive in that direction.

An example LiDAR scan is shown below, visualized with the <a href="https://matplotlib.org" target="_blank">matplotlib</a> library. The blue points trace out the detected obstacles. The black arrow represents the direction the robot will travel - the direction with the least amount of obstacles.

<img src="/assets/images/lidar_scan.png" alt="A plot of an example LiDAR scan." style="
    display: block;
    margin-right: auto;
    margin-left: auto;
    width: 40%;
    "
/>



### Limitations

In the current implementation of obstacle avoidance, there are two main limitations: (1) the mounting of the LiDAR and (2) the update rate of drive commands. On the current chassis, the LiDAR is mounted relatively high. Since it is only a 2D LiDAR, the algorithm misses any obstacles lower than its height, which is a fair amount, especially in a household environment. This leads to incorrect behavior where the robot bumps into obstacles.

The other limitation is the update rate of the drive commands themselves. In the current implementation of the Arduino interface, if two messages are sent in quick succession, they are analyzed as one message, which doesn’t map to a valid drive command, leading to no motion. To adjust for this, we slowed down the frequency of LiDAR-based drive commands. While this ensures that the Arduino interface behaves as expected, it does mean that the update rate is limited, causing delays during the sudden appearance of an obstacle, or hitting obstacles in tight spaces that require quick reactions.

