FROM osrf/ros:galactic-desktop

ENV ROS_DISTRO=galactic

# Install ros2 gazebo packages
RUN apt-get update &&\
    sudo apt-get install -y ros-$ROS_DISTRO-gazebo-ros \
    ros-$ROS_DISTRO-gazebo-plugins \
    ros-$ROS_DISTRO-gazebo-ros-pkgs

# # Install Navigation2
# RUN apt-get update &&\
#     apt-get install -y ros-$ROS_DISTRO-navigation2 \
#     ros-$ROS_DISTRO-nav2-bringup  

# # Install Groot dependencies
# RUN apt-get update &&\
#     apt-get install -y qtbase5-dev \
#     libqt5svg5-dev \
#     libzmq3-dev \
#     libdw-dev

# Install husky from source
WORKDIR /root/husky_ws/src
RUN git clone -b $ROS_DISTRO-devel https://github.com/husky/husky.git
# RUN git clone https://github.com/BehaviorTree/Groot.git
WORKDIR /root/husky_ws

RUN apt-get update &&\
    # This seems to be required for gazebo to work (not included in the repo)
    apt-get install -y ros-$ROS_DISTRO-gazebo-ros2-control &&\
    apt-get install -y ros-galactic-teleop-twist-keyboard

# Build
RUN . /opt/ros/$ROS_DISTRO/setup.sh &&\
    apt-get update &&\
    rosdep install -y --from-paths src --ignore-src &&\
    colcon build --symlink-install

COPY README.md /root/husky_ws

RUN apt-get update &&\
    apt-get install tree

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
