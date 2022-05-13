FROM osrf/ros:galactic-desktop

ENV ROS_DISTRO=galactic

# Install Turtlebot3 from source
WORKDIR /root/turtlebot3_ws/src
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
RUN git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
RUN git clone https://github.com/BehaviorTree/Groot.git
WORKDIR /root/turtlebot3_ws

# Build
RUN . /opt/ros/$ROS_DISTRO/setup.sh &&\
    apt-get update &&\
    rosdep install -y --from-paths src --ignore-src &&\
    colcon build --symlink-install

ENV TURTLEBOT3_MODEL=burger
ENV MAP_PATH=/root/turtlebot3_ws/src/turtlebot3/turtlebot3_navigation2/map/turtlebot3_world.yaml

# Install ros2 gazebo packages
RUN apt-get update &&\
    sudo apt-get install -y ros-$ROS_DISTRO-gazebo-ros \
    ros-$ROS_DISTRO-gazebo-plugins \
    ros-$ROS_DISTRO-gazebo-ros-pkgs

# Install developer tools
RUN apt-get update &&\
    apt-get install tree

# Dist-upgrade is recommended for ROS dockers. See https://github.com/ros2/rosidl/issues/680
RUN apt-get update &&\
    apt-get dist-upgrade -y 

COPY README.md /root/turtlebot3_ws

# Add source turtlebot3_ws to .bashrc
RUN echo 'source ~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc
RUN echo 'echo "ran source ~/turtlebot3_ws/install/setup.bash"' >> ~/.bashrc

# Add ros source command to bashrc
RUN echo 'source /opt/ros/$ROS_DISTRO/setup.bash' >> ~/.bashrc
RUN echo 'echo "ran source /opt/ros/$ROS_DISTRO/setup.bash"' >> ~/.bashrc

# Add gazebo source command to bashrc
# Note: gazebo fails to spawn turtlebot the first time if this is not added
RUN echo 'source /usr/share/gazebo/setup.sh' >> ~/.bashrc
RUN echo 'echo "ran source /usr/share/gazebo/setup.sh"' >> ~/.bashrc

# Add symbolic link for running groot to path
RUN ln -s /root/turtlebot3_ws/build/groot/Groot /usr/local/bin/groot

# to simulate
# https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/
