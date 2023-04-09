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

source setup.bash   # sourcing setup.bash
```
Setting up ROS2 evironment means that sourcing `setup.bash`. It is important to set up ROS2 environment for starting to use ROS2. We will add this initializing in bashrc to avoid sourcing this bash single time whenever we use ROS2. Open another terminal
```
source /opt/ros/humble/setup.bash   # test

gedit ~/.bashrc     # open barshrc file
```
Add this `source /opt/ros/humble/setup.bash` at the end of bashrc file and save it. Then we can start using ROS2 whenever opening terminal.

### 1-2 Launch a ROS2 prgram
Open terminator, split two vertical;
In the first terminator;
```
ros2<space><tab><tab>
### >You will see action, launch, node, run

ros2 run demo_nodes_cpp talker      # run talker nodes
```
In the second terminator;
```
ros2 run demo_nodes_cpp listener      # run listener nodes
```

## 2 - Write ROS2 Program/Node
In this section, we will create ROS2 `workspace` in which ROS2 `package` would also be created. Then write the `node` inside the package, and then compile it and run it.
To write ROS2 Program, it is needed to install ROS2 build tool (colcon) with ```sudo apt install python3-colcon-common-extensions```.
There is one more thing needed to do with colcon; it is to source the colcon bash in bashrc.
Open terminal;
```
cd /usr/share/colcon_argcomplete/hook/
ls
### colcon-argcomplete.bash  colcon-argcomplete.zsh

gedit ~/.bashrc     # open the bashrc to source bash file
```
At the end line of bashrc, source bash by adding ```source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash```.

### 2.1 Create ROS2 workspace
To create ROS2 workspace, make directory of ROS2 worksapce under home; open terminator;
```
cd      # make sure home dir
ls

mkdir ros2_ws     # make ros2 workspace directory
ls

cd ros2_ws        
ls
mkdir src         # make src under ros2_ws
ls
### >src

build colcon    # build the ws using colcon
ls
### >build  install  log  src

cd install
ls
### >You will see some setup/bash files. It's important to care is local_setup.bash & setup.bash.
```
The difference between `local_setup.bash` and `setup.bash` is that sourcing local_setup `source local_setup.bash` means overlay and using whatever created under that workspace, but sourcing `setup.bash` means that using the created workspace plus underlay workspace which is global installed ROS2. So, it is highly recommended to source this `setup.bash` in bashrc. Open separate terminator;
```
gedit ~/.bashrc

### Add this and save->> source ~/ros2_ws/install/setup.bash
```


### 2.2 Create a Python & C++ Package
To create a ROS2 Node, we need a Package inside the created Workspace. Packages allow us to separate our code to reusable blocks. Packages are independent, i.e one package is for Camera, one package is for Motion Planning, and another is for Hardwar Control.
To create a package, open terminator/terminal;

**Python Package**
```
cd ros2_ws/src    # cd to ros2_ws/src

ros2 pkg create my_py_pkg --build-type ament_python --dependencies rclpy      # Create ROS2 python package

ls    # check created package
### > my_py_pkg
```

*After created Package, then compile the created package; Open Terminal;*
```
cd ros2_ws/   # chage directory

colcon build      # compile if there is only one or all pkg

## OR ##

colcon build --packages-select my_py_pkg    # compile by selecting desired package
```

**CPP Package**
```
cd ros2_ws/src/     # cd to src
ls

ros2 pkg create my_cpp_pkg --build-type ament_cmake --dependencies rclcpp     # Create ROS2 C++ Package

ls
### > my_cpp_pkg  my_py_pkg
```
*After created Package, then compile the created package; Open Terminal;*
```
cd ros2_ws/

colcon build      # compile all packages

## OR ##

colcon build --packages-select my_cpp_pkg       #  compile by selecting desired package
```
