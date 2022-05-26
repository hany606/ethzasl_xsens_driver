# Xsens ROS2 Docker


This dockerfile is created in order to run this package in ros2 via ros1_ros2_bridge


You need to create main directory <abs_path_main_dir>, have three ws:

- ros1_ros2_bridge_ws: clone ```git clone -b galactic https://github.com/ros2/ros1_bridge.git```

- ros1_ws: to include anything for ros1 (e.g. this package)

- ros2_ws: to include anything for ros2

```bash
docker build -t <name> .


# ----------------------------------------------------
# Source: https://industrial-training-master.readthedocs.io/en/melodic/_source/session7/ROS1-ROS2-bridge.html

# shell 1: ros2 shell
docker run -it -v <abs_path_main_dir>:<mapped_abs_path_main_dir_in_container> --privileged --volume "/dev/ttyUSB0":"/dev/ttyUSB0" --device="/dev/ttyUSB0" <name>

# Example:
docker run -it --rm -v /home/hany606/ros1_ros2_test:/home/main_ws --privileged --volume "/dev/ttyUSB0":"/dev/ttyUSB0" --device="/dev/ttyUSB0" hany606/ros1_ros2_test

. /opt/ros/galactic/setup.bash
cd <ros2_ws>

colcon build
. install/setup.bash

# And do whatever you want with ros2

# ----------------------------------------------------
# shell 2:
# To get the id of the container
docker ps
# get the <id>

docker exec -it <id> bash

. /opt/ros/noetic/setup.bash

cd <ros1_ws>

catkin build
source devel.setup.bash

roslaunch xsens_driver xsens_driver.launch

# ----------------------------------------------------
# shell 3: ros1_ros2_bridge
# To get the id of the container
docker ps
# get the <id>

docker exec -it <id> bash

. <ros1_ws>/devel/setup.bash
. <ros2_ws>/install/setup.bash


cd <ros1_ros2_bridge_ws>

. /opt/ros/galactic/setup.bash colcon build --packages-select ros1_bridge --cmake-force-configure --cmake-args -DBUILD_TESTING=FALSE

. install/setup.bash

ros2 run ros1_bridge dynamic_bridge --bridge-all-topics

```