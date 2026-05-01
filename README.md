# TurtleBot4 Simulation Guide (ROS2 + Gazebo)

Autonomous Mobile Robots Course  
Teaching Assistant: Mohammad

This guide explains how to run the TurtleBot4 simulation used in the
Autonomous Mobile Robots course.

The goal is to help students quickly install, run, and control the robot
in simulation using ROS2 and Gazebo.

---

## System Requirements

Recommended system:

Ubuntu 24.04  
ROS2 Jazzy  
Gazebo Sim

Minimum hardware:

- 8 GB RAM
- OpenGL capable GPU

---

## Workspace Structure

The TurtleBot4 environment is organized as a ROS2 workspace.

Example structure:

turtlebot4_ws
├── src
├── build
├── install
└── log

Meaning:

src  
contains source packages

build  
contains compiled files

install  
contains executable environment

log  
build logs

---

## First Time Setup

If you cloned the repository, you must build the workspace.

Step 1 — go to workspace

cd ~/turtlebot4_ws

Step 2 — load ROS2 environment

source /opt/ros/jazzy/setup.bash

Step 3 — install missing dependencies

rosdep install --from-paths src -yi

Step 4 — build workspace

colcon build

---
## Quick Start 
robot turtlebot

ros2 launch/turtlebot4_gz_bringup turtlebot4_gz.launch.py

Terminal 2:

robot turtlebot

ros2 run teleop_twist_keyboard teleop_twist_keyboard
---

## Activate the Environment

Before running the simulator you must load the environment.

Option 1 — standard ROS method

source /opt/ros/jazzy/setup.bash  
source install/setup.bash

Option 2 — simplified command (if configured)

robot turtlebot

---

## Running the Simulation

Launch TurtleBot4 in Gazebo.

ros2 launch turtlebot4_gz_bringup turtlebot4_gz.launch.py

This command starts:

- Gazebo simulator
- TurtleBot4 robot model
- ROS2 interface

---

## Controlling the Robot

Open a second terminal.

Load the environment again.

robot turtlebot

Then run:

ros2 run teleop_twist_keyboard teleop_twist_keyboard

Use the keyboard keys displayed on the screen to move the robot.

The robot receives commands through the topic:

/cmd_vel

---

## Useful ROS Commands

List active nodes:

ros2 node list

List topics:

ros2 topic list

Check robot velocity commands:

ros2 topic echo /cmd_vel

Check laser scanner data:

ros2 topic echo /scan

---

## Common Problems

### Problem 1 — Package not found

Example error:

Package 'turtlebot4_gz_bringup' not found

Cause:

workspace environment not loaded.

Solution:

source /opt/ros/jazzy/setup.bash  
source install/setup.bash

or

robot turtlebot

---

### Problem 2 — Workspace not built

If the workspace was cloned but not built.

Solution:

cd ~/turtlebot4_ws

source /opt/ros/jazzy/setup.bash

colcon build

---

### Problem 3 — Missing dependencies

Solution:

rosdep install --from-paths src -yi

---

### Problem 4 — Gazebo does not open

Possible causes:

- graphics driver issues
- missing Gazebo packages
- environment not sourced

Try:

robot turtlebot  
ros2 launch turtlebot4_gz_bringup turtlebot4_gz.launch.py

---

## Debugging Tips

If something does not work, check:

1. ROS2 installed correctly  
2. workspace built  
3. environment sourced  
4. correct terminal commands used

Most issues come from step 2 or 3.

---

## Quick Start (Fast Method)

robot turtlebot

ros2 launch turtlebot4_gz_bringup turtlebot4_gz.launch.py

Open a second terminal:

robot turtlebot

ros2 run teleop_twist_keyboard teleop_twist_keyboard

---

## Learning Goals

Students should understand:

- ROS2 nodes
- topics and messages
- robot control using /cmd_vel
- basic Gazebo simulation

This simulation is used to demonstrate how mobile robots interact with
ROS-based control systems.

---

## Support

If you encounter problems:

1. check the common problems section
2. verify your workspace setup
3. contact the course teaching assistant if needed
---

## Class File Example

This example moves the robot forward for 3 seconds and stops for 2 seconds in a loop.

Run in a new terminal after starting the simulation:

```bash
source /opt/ros/jazzy/setup.bash
source ~/turtlebot4_ws/install/setup.bash
python3 ~/turtlebot4_ws/simple_motion.py
