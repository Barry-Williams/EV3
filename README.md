# EV3 example code

```python
#!/usr/bin/env pybricks-micropython
# Add the modules we need to control the robot
# We don't need all of these
from pybricks.hubs import EV3Brick
from pybricks.ev3devices import (Motor, TouchSensor, ColorSensor,
                                 InfraredSensor, UltrasonicSensor, GyroSensor)
from pybricks.parameters import Port, Stop, Direction, Button, Color
from pybricks.tools import wait, StopWatch, DataLog
from pybricks.robotics import DriveBase
from pybricks.media.ev3dev import SoundFile, ImageFile

# Initialize the EV3 Brick.
ev3 = EV3Brick()

# Initialize the motors.
# Check motor connected and port correct
left_motor = Motor(Port.B)
right_motor = Motor(Port.C)
arm_motor = Motor(Port.A)

# Initialize the drive base.
robot = DriveBase(left_motor, right_motor, wheel_diameter=55.5, axle_track=104)

# Initialize sensors
# If sensors are not connected  or port not correct it will cause your program to crash 
# Delete or # out sensors not connected (press Ctrl + /)
gyro = GyroSensor(Port.S1)
# colour = ColorSensor(Port.S2)
# distance = UltrasonicSensor(Port.S3)
# touch = TouchSensor(Port.S4)

# Create function for gyroTurn
LEFT = -1 # Left negative
RIGHT = 1 # Right positive
def turn(direction, angle, speed=50):
    gyro_sensor.reset_angle()
    while gyro_sensor.angle() < angle and gyro_sensor.angle() > angle * -1 :
        right_motor.run(speed * direction)
        left_motor.run(speed * direction * -1)
    right_motor.stop()
    left_motor.stop()

#Examples
turn(LEFT, 90)      # Turn left 90 degrees at speed 50
turn(RIGHT, 120)    # Turn right 120 degrees at speed 50
turn(LEFT, 90, 20)  # Turn left 90 degrees at speed 20
turn(RIGHT, 20, 10) # Turn right 20 degrees at speed 10

arm_motor.run_until_stalled(-1000) # Raise arm until it cannot go up any more (sometimes this needs to be 1000)
arm_motor.reset_angle(0)           # Reset the angle to zero this is useful to set start position at zero degrees (this only need to be done once at the start of the program

# I want you to experiment with the code that you can find by typing the following
robot.
arm_motor.
gyro.
# Remember you can put you mouse over a command for more information
# Feel free to experiment and see what things do (have someone ready to catch the robot)
# If you want code to temporarily not run you can put the # symbol in front of it or
# Press Ctrl + / while on the line or multiple lines selected
# See below if you want to get information from the robot (angles, or other information) to print to the screen
# Can you get the robot to: drive in a square 50cm on each side.
#                           drive around the triangle
#                           Cuboid
# You might want to google python loops




































robot.straight(1000) # Go 1 Meter forward
robot.straight(-1000) # Go 1 Meter backward
arm_motor.run_until_stalled(-1000) # Raise arm until it cannot go up any more (sometimes this needs to be 1000)
arm_motor.reset_angle(0) # Reset the angle to zero this is useful to set start position at zero degrees 
arm_motor.run_target(2000, 220) # Lower arm 220 degrees which should just be just off the ground 

```

### How can I see information from the robot
```python
robot.angle()
arm_motor.angle()
gyro.angle()
```
You may have found the above commands which will give us information from the robot and it's sensors
However if you just type this in it will not do anything
We need to tell python to display this information
We can do this 2 ways
```python
print(robot.angle())           # Will display the estimated robot angle to the output of window in VS Code
ev3.screen.print(gyro.angle()) # Will display the gyro angle on the robot screen
```
The other issue we have is this will only happen once and then not give an updated value we can use a loop to continue to show us the current value
```python
while True:
    arm_motor.run(200)
    print(arm_motor.angle())
```
This will run the arm motor slowely and display the angle to the screen (press the stop ◻ other wise this will run forever)
```python
while True:
    gyro.angle()
```

### There is more info at https://pybricks.com/ev3-micropython/ (but it can be a bit hard to understand)

