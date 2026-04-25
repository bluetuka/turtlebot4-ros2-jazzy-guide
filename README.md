# TurtleBot4 Simulation Guide (ROS2 Jazzy)

Autonomous Mobile Robots Course  
Teaching Assistant: Mohammad

---

## Overview

This guide provides a step-by-step procedure to run and control the TurtleBot4 simulation using ROS2 Jazzy and Gazebo.

The objective is not only to execute the simulation, but also to develop a clear understanding of how ROS2-based robotic systems operate in practice.

---

## System Requirements

### Recommended
- Ubuntu 24.04  
- ROS2 Jazzy  
- Gazebo Sim  

### Minimum
- 8 GB RAM  
- OpenGL-capable GPU  

---

## Workspace Structure

turtlebot4_ws  
├── src  
├── build  
├── install  
└── log  

| Folder   | Description             |
|----------|-------------------------|
| src      | Source packages         |
| build    | Compiled files          |
| install  | Executable environment  |
| log      | Build logs              |

---

## First-Time Setup

cd ~/turtlebot4_ws  
source /opt/ros/jazzy/setup.bash  
rosdep install --from-paths src -yi  
colcon build  

---

## Activate the Environment

source /opt/ros/jazzy/setup.bash  
source install/setup.bash  

Note: "robot turtlebot" is a custom alias.

---

## Running the Simulation

ros2 launch turtlebot4_gz_bringup turtlebot4_gz.launch.py  

---

## Controlling the Robot

Open a second terminal:

robot turtlebot  
ros2 run teleop_twist_keyboard teleop_twist_keyboard  

Control topic: /cmd_vel  

---

## System Architecture Overview

Core components:

- Control Node → handles motion  
- Sensor Nodes → LiDAR, IMU, joints  
- Odometry → position estimation  
- Simulation (Gazebo) → environment  

---

## Navigation Overview

- Global planner  
- Local planner  
- Costmaps  
- Controller  

---

## SLAM

Inputs:
- /scan  
- /odom  

Outputs:
- Map  
- Pose  

---

## Teleoperation

Keyboard → velocity commands  

Topic:
/cmd_vel  

---

## Useful Commands

ros2 node list  
ros2 topic list  
ros2 topic echo /scan  
ros2 topic echo /cmd_vel  

---

## Common Problems

1. Environment not sourced  
2. Workspace not built  
3. No /scan data  
4. Robot not moving  

---

## Quick Start

Terminal 1:
ros2 launch turtlebot4_gz_bringup turtlebot4_gz.launch.py  

Terminal 2:
ros2 run teleop_twist_keyboard teleop_twist_keyboard  

---

## Learning Goals

- ROS2 nodes  
- Topics  
- Robot control  
- Simulation workflow  

---

## Notes

- Always source environment  
- Do not modify src/ packages  
- Most errors come from setup issues  

update check
999
---

## Setup Instructions

Clone the repository:

```bash
git clone https://github.com/bluetuka/turtlebot4-ros2-jazzy-guide.git
cd turtlebot4-ros2-jazzy-guide
cd src

git clone https://github.com/turtlebot/turtlebot4.git
git clone https://github.com/turtlebot/turtlebot4_desktop.git
git clone https://github.com/turtlebot/turtlebot4_simulator.git

cd ..
source /opt/ros/jazzy/setup.bash
rosdep install --from-paths src -yi
colcon build
source install/setup.bash
ros2 launch turtlebot4_gz_bringup turtlebot4_gz.launch.py
