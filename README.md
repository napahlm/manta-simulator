# manta-simulator

Will add a customized UUV simulator later.

# Setup

## 1. ROS Melodic

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
echo "source catkin_ws/devel/setup.bash" >> ~/.bashrc
```
4. Close current terminal

## 4. The UUV simulator

1. Enter the package folder and clone the repository from their github

```
cd ~/catkin_ws/src
git clone https://github.com/uuvsimulator/uuv_simulator.git
```

2. Run this to add the lines sourcing the environment variables to `~/.bashrc`.

```
echo 'source /usr/share/gazebo-9/setup.sh' >> ~/.bashrc
echo 'source /opt/ros/melodic/setup.bash' >> ~/.bashrc
echo 'source $HOME/catkin_ws/devel/setup.bash' >> ~/.bashrc
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

## 5. The Custom Manta Model
