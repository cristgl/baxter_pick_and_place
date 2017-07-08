# baxter_pick_and_place

This repository presents various demonstrations of pick and place tasks with the Baxter research robot. It contains object recognition and manipulation with different focus areas such as various shapes, sizes, and colours. It also includes trajectory and motion planning and the use of different grippers with the physical robot and in the simulation with gazebo, too. The demonstrations, based upon a project from Abhishek Patil from the Northwestern University. 

##Prerequisites

    ###Workstation Setup

    The required steps to setup your workstation are described in the tutorial from rethink robotics®. This include the installation of Ubuntu, ROS, the Baxter SDK and the first connection to the robot. The direct connection from the Baxter to your workstation also requires a network connection from the type Ethernet.
    Example: Network Connection->Add->Ethernet
    Connection name: Baxter
    IPv4 Settings: Method: Manual
    Address: 169.254.0.10, Netmask: 255.255.0.0, Gateway: 0.0.0.0
    <http://sdk.rethinkrobotics.com/wiki/Workstation_Setup>
    
    ###MoveIt

    MoveIt is used for the motion planning, manipulation and collision checking.
    <http://sdk.rethinkrobotics.com/wiki/MoveIt_Tutorial>
    Moreover the package moveit_python by Michael Ferguson need to be installed.
    
    ###Gazebo (optional)

    Gazebo is a powerful simulation tool for robots. It allows to use already existing robots like the Baxter or to create own one. It is very useful for people who have not the possibility to work with a physical robot.
    <http://sdk.rethinkrobotics.com/wiki/Using_Gazebo_and_Baxter>
    It is more comfortable to have a separate workspace for the physical robot and the visual one in the simulation. It is for example not necessary to change everytime the baxter.sh file. The tutorial from the github repository zengzhen explains the steps and it is a good way to get in touch with gazebo.
    <https://github.com/zengzhen/zhen_baxter_moveit>
    If MoveIt is already installed the packages must be copied from the workspace ros_ws in the src folder from ros_gazebo_master. But to use the simulation from this website don't modify the following line from baxter_world.launch.
    <arg name="world_name" value="$(find baxter_gazebo)/worlds/baxter.world"/>
    
    ###Robot arm calibration

    The calibration of the arms is recommend to get precisely results. There are two different calibration routines which are very well described on the website from rethink robotics.
    <http://sdk.rethinkrobotics.com/wiki/Arm_Calibration>
    
    ###Table position and zero point in MoveIt

    It is very annoying to find every time you change the position of the robot or the used table to get the right sizes and coordinates manually for the simulation in MoveIt. There are two programs which make this task easier. The first one is used to get the distance from the ground to the zero point from the reference frame "base" from MoveIt. This value is allways the same if the robot position doesn't change. The table height must be smaller then 0.9 m and known to get this distance. (Watch the video)
    Download the package to get the zero point!

    Then you can continue with the second program which find the size and the position of the used table. At first add the measured distance from the task before.
    Download the package to get the table size and position!
    
    ###The color of the objects

    The object recognition can only work if the colors of the objects are known. The colors are defined in the baxter_img.cpp file as low and high hsv values. The example colored_papers.pdf include three different colors with the related hsv values. They can be printed and used for a first test to recognize them. Download the colored papers!
    But this arent the exactly values because it depends on the printer settings, the ink, the paper etc. The best way to get the color values from an object which should be detected is to take pictures with the Baxter camera from it on the workspace in different positions. This can be in the shadow from something or at a highly illuminated area. Moreover it is recommend to have every time all the used colors on every picture to see if only the one color will be detected with the specific hsv values.

    $ rosrun image_view image_view image:=/cameras/right_hand_camera/image

    This command open a window with a stream of images from Baxter's right hand camera and allows to save images by right-clicking on the display window.
    Then the images can be analyzed with the hsvThresholder.py file. Open a new terminal and execute the python file from the location where it is saved.

    $ python hsvThresholder.py frame0000.jpg
    
    ###Camera calibration and other parameters

    The camera calibration is allways necessary because every camera is differemt. The parameters can be determined with the Camera Calibration Toolbox for Matlab. The website explains the calibration and optimization from a camera with a printed checkerboard. The first calibration example can be done with an example based on a total of 20 images to learn the process. Another option without the software Matlab is the tutorial Camera Calibration and 3D Reconstruction from OpenCV. The parameters must be changed in the baxter_img.cpp file which is in the package from the projects. Further changes which depends on the size of the detected objects can be found in the Readme.txt document from the projects.




Copyright (C) 2017 Maik Heufekes, 05/07/2017.

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation, either version 3 of the License.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with this program. If not, see <http://www.gnu.org/licenses/>.