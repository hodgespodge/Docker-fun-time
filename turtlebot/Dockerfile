FROM osrf/ros:foxy-desktop

ENV ROS_DISTRO=foxy

# Install ros2 gazebo packages
RUN apt-get update &&\
    sudo apt-get install -y ros-$ROS_DISTRO-gazebo-ros \
    ros-$ROS_DISTRO-gazebo-plugins \
    ros-$ROS_DISTRO-gazebo-ros-pkgs

# Install ros2 Cartographer
RUN apt-get update &&\
    apt-get install -y ros-$ROS_DISTRO-cartographer-ros \
    ros-$ROS_DISTRO-cartographer-ros-msgs \
    ros-$ROS_DISTRO-cartographer-ros-mapping \ 
    ros-$ROS_DISTRO-cartographer-ros-occupancy-grid-map-server

# Install Navigation2
RUN apt-get update &&\
    apt-get install -y ros-$ROS_DISTRO-navigation2 \
    ros-$ROS_DISTRO-nav2-* 

# Install Turtlebot3 from source
WORKDIR /~/turtlebot3_ws/src
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
WORKDIR /~/turtlebot3_ws

RUN . /opt/ros/$ROS_DISTRO/setup.sh &&\
    colcon build --symlink-install

ENV TURTLEBOT3_MODEL=burger

# Add source turtlebot3_ws to .bashrc
RUN echo 'source /~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc

# Add ros source command to bashrc
RUN echo 'source /opt/ros/$ROS_DISTRO/setup.bash' >> ~/.bashrc