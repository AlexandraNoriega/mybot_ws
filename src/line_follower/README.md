# Line Follower TurtleBot

Repository used: https://github.com/sudrag/line_follower_turtlebot.git


## Dependencies

* ROS Kinetic
* Catkin
* roscpp package
* std_msgs package
* message_generation package
* OpenCV

# Introduction
This project uses ROS to simulate a line-following Turtlebot robot in the Gazebo environment using a world designed by the authors.

#Install Turtlebot
First, is necessary install the turtlebot (http://wiki.ros.org/Robots/TurtleBot) using: 
```
 sudo apt-get install ros-kinetic-turtlebot-*
```
After this, we can continue creating our workspace.

# Creating a work space
To build the project run the following steps in a terminal:
- Creating a catkin workspace:
```
mkdir catkin_ws
cd catkin_ws
mkdir src
catkin_make
```
- Cloning the repository.
```
cd ~/catkin_ws/src
git clone https://github.com/LuisC2802/line_follower_turtlebot.git
```

# Setting up the Gazebo
To build the Gazebo world:
 - Add the models.tar.gz to the directory .gazebo/models and extract the tar.gz file.
 ```
cd ~/catkin_ws/src/line_follower_turtlebot
mv models.tar.gz ~/.gazebo/models
cd .gazebo/models
tar --extract --file models.tar.gz
```
 To validate the correct process, in a terminal, start Gazebo:
```
gazebo
```
 You should see in Insert /home/user/.gazebo/models, the current directories in the tar.gz file (Bed, Bathroom, stove).
 
# Setting up the .world file
Now, you should move the FinalHouse.world to the gazebo directory:
```
cd ~/catkin_ws/src/line_follower_turtlebot
sudo mv FinalHouse.world /usr/share/gazebo-7/worlds
```
# Setting up the .launch file
Now, you should move the FinalHouse.launch to the gazebo directory:
```
~/catkin_ws/src/line_follower_turtlebot
sudo mv FinalHouse.launch /opt/ros/kinetic/share/gazebo_ros/launch
```
# Run the world launch
To validate the correct set up of the world, run the world launch in the Gazebo.
```
cd
roslaunch gazebo_ros FinalHouse.launch
```
![GitHub-World](https://user-images.githubusercontent.com/82512521/118070662-ef253e00-b36b-11eb-9b4f-703a12e239c2.png)
# To run
To run the project and see the output in the gazebo world , execute the following steps:
```
cd ~/catkin_ws
source devel/setup.bash
roslaunch line_follower_turtlebot Lfmw.launch
```
![LF-Image](https://user-images.githubusercontent.com/82512521/118071235-031d6f80-b36d-11eb-9fdd-4bd584aa6eee.png)

# Developed by: 
- Luis Carlos Parra Camacho
- Juan Andrés Alzate Ocampo
- Andrés Fernando Rodríguez Bayona
- Amy Alexandra Noriega Quintero
- David Fernando Estacio Quiroz.
