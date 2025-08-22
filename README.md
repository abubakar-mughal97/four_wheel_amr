# Ackermann Robot Simulation (ROS 2 + Gazebo)

This package contains the URDF/Xacro description, controllers, and launch files for simulating an Ackermann-steering robot in **ROS 2 Jazzy** with **Gazebo Harmonic**.

## 📖 Overview

- **Simulation**: Gazebo Harmonic 
- **Robot Description**: URDF + Xacro
- **Controllers**: Ackermann steering controller + velocity controller
- **Visualization**: RViz2 with TF and odometry

## Prerequisites

- ROS 2 Jazzy
- Gazebo Harmonic (`ros_gz_sim`)
- `ros_gz_bridge`
- `ros2_control` and `controller_manager`
- `xacro`

Make sure your ROS 2 environment is sourced:

- source /opt/ros/jazzy/setup.bash

# Build the workspace

- mkdir -p ~/ros2_ws/src
- cd ~/ros2_ws/src
- git clone https://github.com/abubakar-mughal97/four_wheel_amr.git
- cd ~/ros2_ws
- colcon build

# Source the workspace

Always source the workspace in every terminal:

- source ~/ros2_ws/install/setup.bash

# Running the Simulation

This starts Gazebo, spawns the robot, and runs robot_state_publisher:

- ros2 launch robot_description gazebo.launch.py

# Launch the controllers

In a new terminal (don’t forget to source the workspace again):

- ros2 launch robot_controller robot_controller.launch.py

This spawns:

- joint_state_broadcaster
- steering and velocity controllers
- the custom ackermann_controller node

# Rviz Setup
If RViz is not already configured:
1. Add a RobotModel display.
2. Set its Description Topic to /robot_description.
3. Set the Fixed Frame to odom.


# Driving the Robot

Steer the wheels by publishing to the /steering_angle topic (in radians):

- ros2 topic pub /steering_angle std_msgs/msg/Float64 'data: 0.2'

Drive forward/backward by publishing to the /velocity topic (in m/s):

- ros2 topic pub /velocity std_msgs/msg/Float64 'data: 1.0
  '

# TF Frames

- odom → base_footprint is provided by the odometry publisher
- base_footprint → bottom_link → wheel connectors → steering links → wheel links are published by robot_state_publisher
  You should see the robot moving in both Gazebo and RViz.

# Future Improvements
- Control the robot using a joystick 
- Merge both launch files into a single "bringup" launch file.
- Add navigation stack (Nav2) integration.
- Add SLAM (e.g. slam_toolbox) if a LiDAR is mounted.
