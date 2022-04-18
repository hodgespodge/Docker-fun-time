- launch sim (may need to rerun if gazebo is slow to start)
    `ros2 launch husky_gazebo husky_playpen_launch.py`  
    **OR**  
    `ros2 launch husky_gazebo gazebo_launch.py`  

- launch teleop (with topic remaping)
    `ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args --remap /cmd_vel:=/husky_velocity_controller/cmd_vel_unstamped`  

- launch groot  
    `groot`  