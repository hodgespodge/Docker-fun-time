FROM osrf/ros:melodic-desktop-full

ENV ROS_DISTRO=melodic

RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654 &&\
    apt update &&\
    apt install ros-melodic-ros-base

RUN apt-get update &&\
    apt install -y python3-pip &&\
    pip3 install cython &&\
    pip3 install bosdyn-client bosdyn-mission bosdyn-api bosdyn-core &&\
    pip3 install empy

RUN mkdir -p ~/catkin_ws/src

RUN cd ~/catkin_ws/src &&\
    . /opt/ros/melodic/setup.sh &&\
    catkin_init_workspace 

RUN cd ~/catkin_ws/src &&\
    git clone https://github.com/clearpathrobotics/spot_ros.git &&\
    git clone https://github.com/ros/geometry2 --branch 0.6.5

RUN cd ~/catkin_ws/ &&\
    apt-get update &&\
    . /opt/ros/melodic/setup.sh &&\
    rosdep install -y --from-paths src --ignore-src -y

RUN cd ~/catkin_ws/ &&\
    . /opt/ros/melodic/setup.sh &&\
    catkin_make --cmake-args -DCMAKE_BUILD_TYPE=Release -DPYTHON_EXECUTABLE=/usr/bin/python3 -DPYTHON_INCLUDE_DIR=/usr/include/python3.6m -DPYTHON_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython3.6m.so

RUN echo '. /opt/ros/$ROS_DISTRO/setup.sh' >> ~/.bashrc &&\
    echo 'echo "Sourced $ROS_DISTRO"' >> ~/.bashrc 
    
RUN echo '. ~/catkin_ws/devel/setup.bash' >> ~/.bashrc &&\ 
    echo 'echo "Sourced ~/catkin_ws/devel/setup.bash"' >> ~/.bashrc 
