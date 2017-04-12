# AR Drone pose estimation with the ORB-SLAM library
This repository adapts the ORB-SLAM library for pose estimation on the AR-Drone. Scale estimation for the monocular slam process is generated by comparing the ORB-SLAM pose estimate with the altitude estimate published in the /ardrone/navdata topic. There is also efficient collision checking functionality for the point cloud generated by ORB-SLAM. 

The goal of this project is to provide an easy-to-use testbed for motion planning and control research using the AR-Drone
## Packages

### ardrone_autonomy
This is the driver for sending velocity commands from a computer to the AR-Drone and receiving sensor data via wifi connection. It is cloned from the git repo:

[ARdrone driver repo](https://github.com/AutonomyLab/ardrone_autonomy) 

### ardrone_tutorials
This is repo contains a simple keybord controller for manual flight. It is cloned from:

[Keyboard drive repo](https://github.com/mikehamer/ardrone_tutorials)

### ORB_SLAM2
This is the SLAM library that is used for mapping and localization. It is cloned from the git repo:

[Monocular slam repo](https://github.com/raulmur/ORB_SLAM2) 

You will have to follow the setup and compilation instructions in the readme for this package carefully. 

### ardrone_orb
This package is the adaptor for the ORB_SLAM2 library into the ROS catkin framework. The settings.yaml file in this package contains camera calibration parameters for the AR-Drone camera. 

### ardrone_planner_utils
This package contains a collision detection function that organizes the ORB-SLAM point cloud into a kd-tree for efficient distance querries between the ardrone and obstacles detected by ORB-SLAM

## Dependancies
Robot Operating System (ROS): [ROS](http://wiki.ros.org/ROS/Installation)  
Open Computer Vision (OpenCV): [OpenCV](http://opencv.org)  
Eigen3: [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page)  
Pangolin: [Pangolin](https://github.com/stevenlovegrove/Pangolin)  

## Getting Started

1) You should create a local catkin workspace for the packages. Wherever you will have the top level directory run:

```
mkdir ardrone_ws
cd ardrone_ws
mkdir src
cd src 
``` 

2) Clone the project into /ardrone_ws/src/ 

```
cd ardrone_ws/src/

git clone git@github.com:idsc-frazzoli/ardrone_testbed.git
```

3) Compile ORB_SLAM2 (after installing its dependancies: Eigen3, OpenCV, Pangolin):

```
cd ardrone_ws/src/ORB_SLAM2
chmod +x build.sh
./build/sh
```

4) Initialize the catkin_workspace and compile the project:

```
cd /ardrone_ws/src/
catkin_init_workspace
cd /ardrone_ws/
catkin_make
source devel/setup.bash
```

5) Connect to the AR-DRone:

Plug in the AR-Drone and connect to it via Wifi from the computer you plan to run the project from.

6) Launch everything:

roslaunch main.launch

7) To fly the drone with the keyboard drive:

-Put the cursor over the QT gui that pops up for keyboard drive node

Emergency shutdown: Space Bar  
   Takeoff: Y  
      Land: H  
        Up: Q  
      Down: A  
 Turn Left: W  
Turn Right: R  
 Move Left: S  
Move Right: F  
   Forward: E  
  Backward: D  

### For good scale estimation:  
Scale estimation is based on vertical motion so in the first few seconds of flight, flying the AR-Drone vertically will lead to a good scale estimate.
