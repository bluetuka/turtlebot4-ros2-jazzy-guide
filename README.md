# TurtleBot4 Simulation Guide (ROS2 Jazzy)

Autonomous Mobile Robots Course  
Teaching Assistant: Mohammad

---

## Overview

This guide explains how to run and control the TurtleBot4 simulation using ROS2 Jazzy and Gazebo.

The objective is not only to run the simulation, but also to understand how ROS2-based robot systems work in practice.

---

## System Requirements

**Recommended:**

- Ubuntu 24.04
- ROS2 Jazzy
- Gazebo Sim

**Minimum:**

- 8 GB RAM
- OpenGL capable GPU

---

## Workspace Structure

The TurtleBot4 environment follows the standard ROS2 workspace structure:

```bash
turtlebot4_ws
├── src
├── build
├── install
└── log
```

| Folder   | Description                     |
|----------|---------------------------------|
| src      | Source packages                 |
| build    | Compiled files                  |
| install  | Executable environment          |
| log      | Build logs                      |

Understanding this structure is important for debugging and development.

---

## First Time Setup

If you cloned the repository:

```bash
cd ~/turtlebot4_ws
source /opt/ros/jazzy/setup.bash
rosdep install --from-paths src -yi
colcon build
```

---

## Activate the Environment

Before running anything:

```bash
source /opt/ros/jazzy/setup.bash
source install/setup.bash
```

Optional shortcut:

```bash
robot turtlebot
```

---

## Running the Simulation

Launch the simulation:

```bash
ros2 launch turtlebot4_gz_bringup turtlebot4_gz.launch.py
```

This starts:

- Gazebo simulation
- TurtleBot4 robot model
- ROS2 communication interface

---

## Controlling the Robot

Open a second terminal:

```bash
robot turtlebot
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

Control topic:

```
/cmd_vel
```

---

## Understanding the System

This simulation is based on ROS2 concepts:

- Nodes → independent processes  
- Topics → communication channels  
- Messages → data exchanged between nodes  

Example:

```bash
ros2 topic echo /cmd_vel
```

---

## Useful Commands

```bash
ros2 node list
ros2 topic list
ros2 topic echo /scan
ros2 topic echo /cmd_vel
```

---

## Common Problems

### 1. Package not found

```bash
source /opt/ros/jazzy/setup.bash
source install/setup.bash
```

---

### 2. Workspace not built

```bash
cd ~/turtlebot4_ws
colcon build
```

---

### 3. No LiDAR data (/scan empty)

Possible causes:

- Gazebo paused  
- Sensor not initialized  
- Environment not sourced  

Check:

```bash
ros2 topic echo /scan --qos-reliability best_effort
```

---

### 4. Robot does not move

Check:

- Are you using the correct topic? (`/cmd_vel`)  
- Is teleop running?  
- Is simulation running (Gazebo not paused)?  

---

## Debugging Strategy

When something fails:

1. Check environment (source)  
2. Check topics (`ros2 topic list`)  
3. Check data flow (`ros2 topic echo`)  
4. Check simulation state (Gazebo running)  

---

## Quick Start

**Terminal 1:**

```bash
robot turtlebot
ros2 launch turtlebot4_gz_bringup turtlebot4_gz.launch.py
```

**Terminal 2:**

```bash
robot turtlebot
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

---

## Learning Goals

After this exercise, students should understand:

- ROS2 node structure  
- Topic-based communication  
- Robot control using velocity commands  
- Basic simulation workflow in Gazebo  

---

## Example Script

```bash
source /opt/ros/jazzy/setup.bash
source ~/turtlebot4_ws/install/setup.bash
python3 ~/turtlebot4_ws/simple_motion.py
```

This script moves the robot forward for 3 seconds and stops for 2 seconds in a loop.

---

## Notes for Students

- Do not modify system packages inside `src/`  
- Always source the environment before running commands  
- Most issues come from missing setup or incorrect terminal usage  
