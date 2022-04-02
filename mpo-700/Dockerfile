FROM osrf/ros:galactic-desktop

ENV ROS_DISTRO=galactic

### RUNNING SCRIPT COMMANDS FROM: https://github.com/neobotix/robot-setup-tool.git

# Install nav2 and slam toolbox
RUN apt-get update &&\
    apt-get install -y ros-$ROS_DISTRO-navigation2 ros-$ROS_DISTRO-nav2-* ros-$ROS_DISTRO-slam-toolbox

# Install Teleop-joy
RUN apt-get update &&\
    apt-get install -y ros-$ROS_DISTRO-teleop-twist-joy ros-$ROS_DISTRO-teleop-twist-keyboard

# Install Groot dependencies
RUN apt-get update &&\
    apt-get install -y qtbase5-dev \
    libqt5svg5-dev \
    libzmq3-dev \
    libdw-dev

RUN rosdep update

WORKDIR /mpo_700_workspace/src

RUN git clone --branch $ROS_DISTRO  https://github.com/neobotix/neo_mpo_700-2.git
RUN git clone --branch $ROS_DISTRO  https://github.com/neobotix/neo_local_planner2.git
RUN git clone --branch master       https://github.com/neobotix/neo_common2
RUN git clone --branch $ROS_DISTRO  https://github.com/neobotix/neo_relayboard_v2-2
RUN git clone --branch $ROS_DISTRO  https://github.com/neobotix/neo_kinematics_omnidrive2.git
RUN git clone --branch $ROS_DISTRO  https://github.com/neobotix/neo_sick_s300-2
RUN git clone --branch $ROS_DISTRO  https://github.com/neobotix/neo_teleop2
RUN git clone --branch master       https://github.com/neobotix/neo_msgs2
RUN git clone --branch master       https://github.com/neobotix/neo_srvs2
RUN git clone --branch $ROS_DISTRO  https://github.com/neobotix/neo_localization2.git
RUN git clone                       https://github.com/ros-tooling/topic_tools.git
RUN git clone https://github.com/BehaviorTree/Groot.git

# RUN rosdep update
WORKDIR /mpo_700_workspace
RUN . /opt/ros/$ROS_DISTRO/setup.sh &&\
    rosdep install --from-paths src/Groot --ignore-src &&\
    colcon build --symlink-install

RUN echo 'export LC_NUMERIC="en_US.UTF-8"' >> ~/.bashrc
RUN echo 'source /opt/ros/$ROS_DISTRO/setup.bash' >> ~/.bashrc
### DONE RUNNING SCRIPT COMMANDS

RUN echo 'source /mpo_700_workspace/install/setup.bash' >> ~/.bashrc
RUN apt-get update &&\
    apt-get install -y ros-$ROS_DISTRO-neo-simulation2

# Install ros2 gazebo packages
RUN apt-get update &&\
    sudo apt-get install ros-$ROS_DISTRO-gazebo-ros ros-$ROS_DISTRO-gazebo-plugins ros-$ROS_DISTRO-gazebo-ros-pkgs

# Add gazebo source command to bashrc
RUN echo 'source /usr/share/gazebo/setup.sh' >> ~/.bashrc
RUN echo 'echo "ran source /usr/share/gazebo/setup.sh"' >> ~/.bashrc

RUN apt-get update &&\
    apt-get install tree

RUN ln -s /mpo_700_workspace/build/groot/Groot /usr/local/bin/groot


ENV MY_ROBOT=mpo_700
ENV MAP_NAME=neo_workshop

# Commands to run

# https://neobotix-docs.de/ros/ros2/simulation.html
# https://neobotix-docs.de/ros/ros2/autonomous_navigation.html