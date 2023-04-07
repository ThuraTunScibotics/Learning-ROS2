# Learning-ROS2

## 1 - Installation
- I use ROS2 Humble: https://docs.ros.org/en/humble/Installation.html
- Install terminator: ```sudo apt install terminator```
- Install python3-pip ```sudo apt install python3-pip```
- Install `VS code` IDE, and add extension of `c++`, `python` and `cmake`.

### 1-1 Setup environment for ROS2
We need to setup ROS2 evironmen in basrc to eable glabal running of ROS2 whenever we open terminal.
To check `setup.bash` location, run the following in terminal;
```
cd /opt/ros   # locate ROS
ls

cd humble
ls

source setup.bash
```
Setting up ROS2 evironment means that sourcing `setup.bash`. It is important to set up ROS2 environment for starting to use ROS2. We will add this initializing in bashrc to avoid sourcing this bash single time whenever we use ROS2.
```
source /opt/ros/humble/setup.bash

gedit ~/.bashrc
```
Add this `source /opt/ros/humble/setup.bash` at the end of bashrc file and save it. Then we can start using ROS2 whenever opening terminal.
