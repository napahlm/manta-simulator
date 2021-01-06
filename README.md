# Mantabantalanta

Will add a customized UUV simulator later.

Known problems:
1. Gazebo doesn't shut down (or takes way too long) when you kill the node which started the program. Rapid use of the `roslaunch` command and killing it again might therefore not work, and new simulations are waiting indefinitely for the last one to shut down. *Restarting your PC seems to work fine.*

# Complete Setup

You only need a working Linux desktop running Ubuntu 18.04 LTS.

Tip: Copy/paste in the Ubuntu terminal is by default
```
Ctrl + Shift + C
```
```
Ctrl + Shift + V
```


## 1. ROS Melodic

Detailed walkthrough: http://wiki.ros.org/melodic/Installation/Ubuntu


1. Set up sources.list

```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

2. Set up keys

```
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```

3. Install ROS

```
sudo apt update
```

```
sudo apt install ros-melodic-desktop-full
```

4. Set up environment

```
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

5. Install dependencies

```
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
```

5.1 Initialize rosdep

```
sudo apt install python-rosdep
```

```
sudo rosdep init
rosdep update
```

## 2. Dependancies

```
sudo apt install protobuf-compiler ros-melodic-rosbridge-server ros-melodic-message-to-tf ros-melodic-geographic-msgs ros-melodic-move-base ros-melodic-move-base-msgs
```

## 3. ROS Workspace

0. Catkin tools

```
sudo apt-get update
sudo apt-get install python-catkin-tools
```

1. The catkin workspace

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws
catkin init
```

2. Build the workspace

```
cd ~/catkin_ws
catkin build
```

3. Source the workspace

```
echo 'source $HOME/catkin_ws/devel/setup.bash' >> ~/.bashrc
```
4. Close current terminal

## 4. The UUV simulator

1. Enter the package folder and clone the repository from their github

```
cd ~/catkin_ws/src
git clone https://github.com/uuvsimulator/uuv_simulator.git
```

2. Run this to add the lines sourcing the environment variables to `~/.bashrc`. (The environmen variables for ROS and the workspace are already sourced)

```
echo 'source /usr/share/gazebo-9/setup.sh' >> ~/.bashrc
```

3. Source the `.bashrc`

```
source ~/.bashrc
```
3.1. Trouble because of another workspace? Try this

```
source ~/catkin_ws/devel/setup.bash
```

4. Build the workspace

```
cd ~/catkin_ws
catkin build
```

## 5. The Manta Model

1. Enter the package folder and clone the repository from github

```
cd ~/catkin_ws/src
git clone https://github.com/napahlm/manta-model.git
```

2. Build the packages

```
cd ~/catkin_ws
catkin build
```

## The Manta Control System
1. Enter the package folder and clone the repository from github

```
cd ~/catkin_ws/src
git clone https://github.com/napahlm/manta-rov.git
```

2. Build the packages

```
cd ~/catkin_ws
catkin build
```

## The Vortex Messages Package

1. Enter the package folder and clone the repository from github

```
cd ~/catkin_ws/src
git clone https://github.com/vortexntnu/vortex_msgs.git
```

2. Build the packages

```
cd ~/catkin_ws
catkin build
```

## Running Different Tests

1. Spawn Manta in a default world to test the simulator (Control system and vortex_msgs NOT needed)

```
roslaunch manta_gazebo start_demo.launch
```

2. Test the control system (Spawn the world and Manta first)

```
roslaunch vortex simulator.launch DOESNT WORK YET
```

# Running the Control System on the Raspberry Pi 4

[This section is still under testing with no clear results yet.]

## Setup

1. Install ROS, but not ros-desktop-full. Barebone should work fine. Might need some extra dependencies.

2. Install the dependencies (Might only be needed for simulator PC)

Weird dependencies needed for RPi:

"osrf-common" is not automatically installed on RPi Ubuntu.

```
sudo apt install python-catkin-tools python-osrf-common
```

3. Configure the workspace as normal

4. IGNORE the simulator

5. IGNORE the model of Manta

6. Git clone the control system as normal

7. Git clone the messages package

8. Build the workspace (Build vortex_msgs first since it's a dependancy kinda)

```
catkin build vortex_msgs
catkin build
```

8. Run custom tests (The entire system this time)
