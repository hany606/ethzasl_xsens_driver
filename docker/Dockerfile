FROM osrf/ros:galactic-desktop

RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

RUN apt install curl # if you haven't already installed curl
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -


RUN apt update &&\
	apt install -y ros-noetic-desktop-full
RUN apt install -y python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential python3-rosdep ros-noetic-catkin python3-catkin-tools python3-osrf-pycommon python-is-python3 python3-pip usbutils


RUN /bin/bash /opt/ros/noetic/setup.bash

#RUN apt update && apt install -y ros-noetic-catkin python3-catkin-tools python3-osrf-pycommon python-is-python3 python3-pip

RUN pip3 install pyserial #serial


#RUN rosdep init && rosdep update



