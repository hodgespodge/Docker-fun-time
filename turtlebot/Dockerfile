FROM osrf/ros:foxy-desktop

ENV ROS_DISTRO=foxy

# Install ros2 gazebo packages
RUN apt-get update &&\
    sudo apt-get install -y ros-$ROS_DISTRO-gazebo-ros \
    ros-$ROS_DISTRO-gazebo-plugins \
    ros-$ROS_DISTRO-gazebo-ros-pkgs

# Install ros2 Cartographer
RUN apt-get update &&\
    apt-get install -y ros-$ROS_DISTRO-cartographer \
    ros-$ROS_DISTRO-cartographer-ros

# Install Navigation2
RUN apt-get update &&\
    apt-get install -y ros-$ROS_DISTRO-navigation2 \
    ros-$ROS_DISTRO-nav2-bringup  

# Install Turtlebot3 from source
WORKDIR /root/turtlebot3_ws/src
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
WORKDIR /root/turtlebot3_ws

RUN . /opt/ros/$ROS_DISTRO/setup.sh &&\
    colcon build --symlink-install

ENV TURTLEBOT3_MODEL=burger
ENV MAP_PATH=/root/turtlebot3_ws/src/turtlebot3/turtlebot3_navigation2/map/turtlebot3_world.yaml

RUN apt-get update &&\
    apt-get install tree

# Add source turtlebot3_ws to .bashrc
RUN echo 'source ~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc
RUN echo 'echo "ran source ~/turtlebot3_ws/install/setup.bash"' >> ~/.bashrc

# Add ros source command to bashrc
RUN echo 'source /opt/ros/$ROS_DISTRO/setup.bash' >> ~/.bashrc
RUN echo 'echo "ran source /opt/ros/$ROS_DISTRO/setup.bash"' >> ~/.bashrc

# to simulate
# https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/
