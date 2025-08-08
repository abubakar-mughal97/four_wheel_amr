Usage (asssuming the necessary ROS2 Jazzy packages are already installed)

Clone the Repository 
cd <your_workspace>
git clone https://github.com/BlackkBeardd/four_wheel_amr.git

 Build the workspace
 cd <your_workspace>
 colcon build

 Launching
 In a separate terminal:
 source install/setup.bash 
 ros2 launch robot_description gazebo.launch.py

 In another terminal:
 source install/setup.bash 
 ros2 launch robot_controller controller.launch.py
 
