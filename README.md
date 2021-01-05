# manta-simulator

Will add a customized UUV simulator later.

# Complete Setup

You only need a working Linux desktop running Ubuntu 18.04 LTS.


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

3. Source the `.bashrc`.

```
source ~/.bashrc
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
[SOON]
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
