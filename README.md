# mybot_ws

**Installation**

This repository represents a workspace. For that reason you should clone the repository in home.

``
git clone https://github.com/AlexandraNoriega/mybot_ws.git
``

Now go to the new workspace and compile it.

``
~/mybot_ws$ catkin_make
``

As it is a new workspace, remember to put on the bash file the direction of devel folder

``
echo "source ~/mybot_ws/devel/setup.bash" >> ~/.bashrc
``

**Package Explanation**

- **line_follower:** contains codes to simulate a line follower, mybot will map the enviroment while is following the line
- **mybot_description:** specifies the entire robot structure as links and joints and launches the model in rviz.
- **mybot_gazebo:** launches the model in the gazebo environment and contains different simulation worlds.
- **mybot_navigation:** launches the gmapping used for SLAM, control the robot movement with teleop keyboard and load the map obtained by gmapping on simulation enviroment. Besides contains the saved maps (.pgm and .yaml)
- **turtlebot:** contains files to launch the teleop spec

**Execution**

1. Run roscore like a pre-requisites of a ROS-based system.

*Run the following lines each in a different terminal*

2. We're going to open gazebo with the load world and robot

``
roslaunch mybot_gazebo mybot_world.launch 
``

3. You can map the enviroment making mybot to follow the yellow line (the world you simulate must have a yellow line (lfm1.world)) or using teleop. 

  - In the first case run

``
roslaunch mybot_navigation gmapping_demo_line.launch
``

  - To start mapping using teleop we will execute a launch file. This line will save the sensor data located in the robot, in this case the robot uses a *Hokuyo laser* 

``
roslaunch mybot_navigation gmapping_demo.launch
``

4. Open rviz to verify the progress of map creation

``
roslaunch mybot_description mybot_rviz_gmapping.launch
``

5. Now link from launch the teleop_keyboard code of Turtlebot to move the robot through the world

``
roslaunch mybot_navigation mybot_teleop.launch
``

6. When you finish touring the map, we proceed to save it. Remember to change the <archive_name> each mapping to not overwrite files

``
rosrun map_server map_saver -f ~/mybot_ws/src/mybot_navigation/maps/<archive_name>
``
The job is done, now we can kill all processes and proceed with slam. 

**SLAM**

We can open the saved maps following the next steps:

1. Edit the map_file. You might open **mybot_navigation/launch/amcl_demo.launch**, get on the sixth line and modify the path changing it for that one choosen in the previous step.
2. Run gazebo for looking the robot at the selected world

``
roslaunch mybot_gazebo mybot_world.launch 
``

3. Load the created map.

``
roslaunch mybot_navigation amcl_demo.launch 
``

4. As execution steps, we are going to visualize the map with rviz and this program will help us to interact with robot movement

``
roslaunch mybot_description mybot_rviz_amcl.launch
``

Now you can distribute the screen between the gazebo and rviz to improve the visualization of the movement and interaction with the map. At top of rviz we see some options like "Interact", "Move camera", "Select", ... , "2D Nav Goal", select the last one and click the place where you want the robot to go, with sustained click you can change the robot orientation.

**Personalize**

If you want to change the world, you can:

- Use a gazebo world installed 
- Use a gazebo world owned

If you choose the second note that you need one file <world_name>.world and one file <world_name>.launch and a third one (model folder) ir the world has models not included at gazebo. You need to copy that file in the following paths

- .world -> opt/ros/kinetic/share/gazebo_ros/launch
- .launch -> usr/share/gazebo-7/worlds
- models -> .gazebo/models

Finally in mybot_gazebo/launch/mybot_world.launch in the 14th line (world_name) replace value="worlds/willowgarage.world" to value="worlds/<world_name>.world"
