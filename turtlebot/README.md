`ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py` 
**OR**
`ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py`

`ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True`
**OR**
`ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True`

[Slam (cartographer) Docs](https://emanual.robotis.com/docs/en/platform/turtlebot3/slam_simulation/)

`ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True`

[Nav Docs](https://emanual.robotis.com/docs/en/platform/turtlebot3/nav_simulation/)

`ros2 run turtlebot3_teleop teleop_keyboard`