# mybot_ws

**Installation**

This repository represents a workspace for that reason you should clone the repository in home.

``
git clone https://github.com/AlexandraNoriega/mybot_ws.git
``

Now go to the created workspace and compile it.

``
~/mybot_ws$ catkin_make
``

As it is a new workspace remember put the direction devel to search path

``
echo "source ~/mybot_ws/devel/setup.bash" >> ~/.bashrc
``

**Execution**

First, run roscore like a pre-requisites of a ROS-based system.

Second, run the following lines each in a different terminal

- We're going to open gazebo with the load world and robot

``
roslaunch mybot_gazebo mybot_world.launch 
``

To start mapping run, this line will save the sensor data located in the robot, in this case the robot use *Hokuyo laser* 

``
roslaunch mybot_navigation gmapping_demo.launch
``

Open rviz to watch the progress of map creation

``
roslaunch mybot_description mybot_rviz_gmapping.launch
``

Now link from launch the teleop_keyboard code of Turtlebot to move the robot through the world

``
roslaunch mybot_navigation mybot_teleop.launch
``

When you finish touring the map, we proceed to save it. Remember change the <archive_name> each mapping so as not to overwrite

``
rosrun map_server map_saver -f ~/mybot_ws/src/mybot_navigation/maps/<archive_name>
``

Kill all the terminals. Is necessary to edit the map_file in the sixth line for load the map in the SLAM similation so go to mybot_navigation/launch/amcl_demo.launch and modify the path changing for the choosen in the previous step

**SLAM**

Run gazebo for looking the robot at the selected world

``
roslaunch mybot_gazebo mybot_world.launch 
``

Load the created map.

``
roslaunch mybot_navigation amcl_demo.launch 
``

As execution steps, we are going to visualize the map with rviz and this program will help us to interact with robot movement

``
roslaunch mybot_description mybot_rviz_amcl.launch
``

Now you can you can distribute the screen between the gazebo and rviz to better visualize the movement and interaction with the map. At top of rviz we see some options like "Interact", "Move camera", "Select", ... , "2D Nav Goal", select the last mentioned and place the mouse at the position where you want the robot to move, hold the click there and direct the arrow so that the robot is looking in that direction

**Personalize**

If you want to change the world, you can:

-Use a gazebo world installed 
-Use a gazebo world owned

If you choose the second note that you need one file <world_name>.world and one file <world_name>.launch and a third one (model folder) ir the world has models not included at gazebo. You need to copy that file in the following paths

- .world -> opt/ros/kinetic/share/gazebo_ros/launch
- .launch -> usr/share/gazebo-7/worlds
- models -> .gazebo/models

By last in mybot_gazebo/launch/mybot_world.launch in the 14th line (world_name) replace value="worlds/willowgarage.world" to value="worlds/<world_name>.world"
