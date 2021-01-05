# manta-simulator

Will add a customized UUV simulator later.

# Setup

## Dependancies

```
sudo apt install protobuf-compiler ros-melodic-rosbridge-server ros-melodic-message-to-tf ros-melodic-geographic-msgs ros-melodic-move-base ros-melodic-move-base-msgs
```
## ROS Workspace

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
echo "source catkin_ws/devel/setup.bash" >> ~/.bashrc
```
4. Close current terminal

## The UUV simulator

1. Enter the package folder and clone the repository from their github

```
git clone https://github.com/uuvsimulator/uuv_simulator.git
```

3. Build the workspace

```
cd ~/catkin_ws
catkin build
```







