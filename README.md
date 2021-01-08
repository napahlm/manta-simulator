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

Quick setup:

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

4. Set up environment variables

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

## 5. The Manta Gazebo Model

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

## The Manta Control System

1. Enter the package folder and clone the repository from github

```
cd ~/catkin_ws/src
git clone https://github.com/napahlm/manta-rov.git
```

2. Build the packages. Make sure "vortex_msgs" is built first.

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

The Raspberry Pi is running Ubuntu Mate 20.04 and ROS Noetic.
This seems to be the only stable and maintained option as the right version of Ubuntu 18.04 for RPi4 is hard to find.

Known challenges running ROS Noetic on a system developed on ROS Melodic:

1. Noetic uses Python3, Melodic uses Python 2.7 (Denoted Python in scripts). Make sure to either configure your Python Path to run Python3 when Python is called, or change Python to Python3 in all ROS python scripts in the first line. (i.e. #!/usr/bin/env python --> #!/usr/bin/env python3)

Known challenges running ROS on the RPi4:

1. Usually ROS is installed without many dependancies because of the weaker processor. These will be added in a list below.

2. Access to the GPIO pins is by default done through the Raspberry Pi OS, but can be done easily on Ubuntu Mate. Normal Ubuntu versions lacks the permissions accessing the pins.

## Setup

0. Ubuntu Mate?

Wait for packages to finish installing (unattended-upgr). Takes a lot of time

Activating SSH:

```
sudo apt update
```
```
sudo apt install openssh-server
```

Verify that it's running with this:

```
sudo systemctl status ssh
```

Enable SSH.

```
sudo ufw allow ssh
```

Configure a static IP and SSH:

[COMING]


1. Install ros-base. Only consider ros-desktop for troubleshooting graphical tools.

http://wiki.ros.org/noetic/Installation/Ubuntu

2. Install the dependencies specific for RPi4.

"osrf-common" is not automatically installed on RPi Ubuntu (Might be the ARM structure)

```
sudo apt install python3-catkin-tools python3-osrf-common
```

"python-is-python3"

Programs for configuring the GPIO pins (libi2c-dev ?)

```
sudo apt install python-is-python3
```

rosdep

```
sudo apt install python3-rosdep
```

```
sudo rosdep init
rosdep update
```

Git

```
sudo apt install git
```

Other

```
sudo apt install ros-noetic-eigen-conversions
```

```
sudo apt install ros-noetic-tf ???
```

```
sudo apt install ros-noetic-roslint
```

Packages: joy

```
sudo apt install ros-noetic-joy
```


3. Configure the workspace using catkin tools.

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin init
```

4. Install the message class

```
cd ~/catkin_ws/src
git clone git clone https://github.com/vortexntnu/vortex_msgs.git
```

5. Install the ROV Control System.

```
cd ~/catkin_ws/src
git clone https://github.com/USERNAME/REPO.git
```

6. Build the packages

```
cd ~/catkin_ws
catkin build vortex_msgs
catkin build
```

8. Run some tests

[Tests are coming.]
