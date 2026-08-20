# mocap4r2_optitrack_driver

[![humble](https://github.com/MOCAP4ROS2-Project/mocap4ros2_optitrack/actions/workflows/humble.yaml/badge.svg)](https://github.com/MOCAP4ROS2-Project/mocap4ros2_optitrack/actions/workflows/humble.yaml)

[![codecov](https://codecov.io/gh/MOCAP4ROS2-Project/mocap4r2_optitrack_driver/humble/graph/badge.svg)](https://codecov.io/gh/MOCAP4ROS2-Project/mocap4r2_optitrack_driver)

Create workspace:
```
mkdir -p mocap4r2_ws/src && cd mocap4r2_ws/src
```
Download optitrack repo:
```
git clone git@github.com:MarineRoboticsGroup/mocap4ros2_optitrack.git
```
Install dependencies:
```
cd ..
rosdep install --from-paths src --ignore-src -r -y
cd src
vcs import < mocap4ros2_optitrack/dependency_repos.repos
```
Compiling workspace:
```
cd .. && colcon build --symlink-install
```
Source workspace:
```
source install/setup.bash
```
Configure Motive networking:

In Motive, open **Settings** and set **Local Interface** to the IP address of the
network interface connected to the OptiTrack system (for example,
`192.168.0.10`). Do not use the loopback address (`127.0.0.1`).

Setup your optitrack configuration:
```
mocap4r2_ws/src/mocap4ros2_optitrack/mocap4r2_optitrack_driver/config/mocap4r2_optitrack_driver_params.yaml
```
Launch optitrack system:
```
ros2 launch mocap4r2_optitrack_driver optitrack2.launch.py
```
Check that Optitrack configuration works fine and is connected. As the driver node is a lifecycle node, you should transition to activate:
```
ros2 lifecycle set /mocap4r2_optitrack_driver_node activate
```
Visualize in rViz:
```
ros2 launch mocap4r2_marker_viz mocap4r2_marker_viz.launch.py mocap4r2_system:=optitrack
```
