FROM osrf/ros:galactic-desktop

ENV ROS_DISTRO=galactic

# # Install Navigation2
# RUN apt-get update &&\
#     apt-get install -y ros-$ROS_DISTRO-navigation2 \
#     ros-$ROS_DISTRO-nav2-bringup  

# Install husky from source
WORKDIR /root/husky_ws/src
RUN git clone -b $ROS_DISTRO-devel https://github.com/husky/husky.git
# RUN git clone https://github.com/BehaviorTree/Groot.git
WORKDIR /root/husky_ws

RUN apt-get update &&\
    apt-get install -y ros-galactic-teleop-twist-keyboard

# Install ros2 gazebo packages
RUN apt-get update &&\
    sudo apt-get install -y ros-$ROS_DISTRO-gazebo-ros \
    ros-$ROS_DISTRO-gazebo-plugins \
    ros-$ROS_DISTRO-gazebo-ros-pkgs

# Build
RUN . /opt/ros/$ROS_DISTRO/setup.sh &&\
    apt-get update &&\
    rosdep install -y --from-paths src --ignore-src &&\
    colcon build --symlink-install

COPY README.md /root/husky_ws

# Install developer tools
RUN apt-get update &&\
    apt-get install tree

# Dist-upgrade is recommended for ROS dockers. See https://github.com/ros2/rosidl/issues/680
RUN apt-get update &&\
    apt-get dist-upgrade -y 


# # Add source husky to .bashrc
RUN echo 'source ~/husky_ws/install/setup.bash' >> ~/.bashrc
RUN echo 'echo "ran source ~/husky_ws/install/setup.bash"' >> ~/.bashrc

# Add ros source command to bashrc
RUN echo 'source /opt/ros/$ROS_DISTRO/setup.bash' >> ~/.bashrc
RUN echo 'echo "ran source /opt/ros/$ROS_DISTRO/setup.bash"' >> ~/.bashrc

# Add gazebo source command to bashrc
# Note: gazebo fails to spawn turtlebot the first time if this is not added
RUN echo 'source /usr/share/gazebo/setup.sh' >> ~/.bashrc
RUN echo 'echo "ran source /usr/share/gazebo/setup.sh"' >> ~/.bashrc

# # Add symbolic link for running groot to path
# RUN ln -s /root/turtlebot3_ws/build/groot/Groot /usr/local/bin/groot
