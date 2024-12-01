
# ROS 2 Humble Image Converter Package 
This repository features the image_conversion_pkg, a ROS 2 package built to showcase image processing capabilities using OpenCV and ROS 2's image_transport. The package subscribes to an image topic, applies processing (such as converting the image to grayscale), and then displays the processed image using OpenCV.

## Table of Contents

1. [Prerequisites](#prerequisites)  
2. [Step-by-Step Procedure for Creating the Workspace](#step-by-step-procedure-for-creating-the-workspace)  
   - [Create the Workspace](#create-the-workspace)  
   - [Clone the Repository](#clone-the-repository)   
   - [Build the Package](#build-the-package)  
3. [Repository Structure](#repository-structure)  
4. [Run the Node](#run-the-node)  
5. [Check the Results](#check-the-results)

## Prerequisites

Before setting up the package, ensure you have the following:

- **ROS 2 Humble Hawksbill**installed. ([Installation Guide](https://docs.ros.org/en/humble/Installation.html))
- **Installation of usb_cam package** 
    ```bash
    sudo apt-get install ros-humble-usb-cam
- OpenCV installed (usually included with `cv_bridge`).  
- `colcon` build tool installed.  
- `image_transport` and `cv_bridge` ROS 2 dependencies.

## Step-by-Step Procedure for creating the workspace
# 1. Create the workspace 
- Create the workspace 
    ````bash
    mkdir -p ~/ros2_ws/src
# 2. Clone the Repository
- Change the path into source directory of the workspace
    ````bash
    cd ~/ros2_ws/src
- Clone the repository from github
    ````bash
    git clone https://github.com/MarthaSuryaTeja/image_conversion_pkg.git
# 3. Build the Package 
- Change the path to ros2_ws directory
    ````bash
    cd ..
- Build the Package
    ````bash
    colcon build
## Repository Structure

Once cloned and set up, your workspace should look like this:
 
         ros2_ws/
         ├── src/
         │   └── image_converter/
         │       ├── CMakeLists.txt
         │       ├── package.xml
         │       └── src/
         │           └── image_converter_node.cpp
                 └── launch
                     └── image_conversion_launch.py
         ├── build/
         ├── install/
         └── log/

## Run the Node
- Open a terminal and source the workspace
    ````bash
    source ~/ros2_ws/install/setup.bash
- Launch the image_conversion node with the following command
    ````bash
    ros2 launch image_converter image_conversion_launch.py
This will start the image_Conversion node and collects the data from the camera

## Check the results
- Open another terminal and paste the below command
    ````bash
    ros2 run rqt_image_view rqt_image_view
This will open a window which show the feed of /camera
### Mode - 1 (Gray Scale Image)
- To check the gray scale converted image. Use below command
    ````bash
    ros2 service call /set_mode std_srvs/srv/SetBool "{data: true}"
- This is the service which is assigned to change the image feed into the gray scale format
- After entering this command, open the rqt_image_view window and change the drop down to /camera/converted_image
![Gray Scale ](https://github.com/user-attachments/assets/207a5162-ac70-4412-87ee-ab2d884efad7)


### Mode - 2 (Coloured Image)
- To change the converted image into Colour, then paste the below command in new terminal
    ````bash
    ros2 service call /set_mode std_srvs/srv/SetBool "{data: false}"
- This is the service which is assigned to change the image feed into the gray scale format
- After entering this command, open the rqt_image_view window and change the drop down to /camera/converted_image

![Color](https://github.com/user-attachments/assets/87d13b60-0cdc-4e90-942a-fe24efcd964c)
