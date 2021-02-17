# Gazebo ROS Link Attacher
This library is used to attach two Gazebo models with a virtual joint in a generalized grasp hack.

## Build
```bash
mkdir -p gazebo_link_attacher_ws/src
cd gazebo_link_attacher_ws/src
catkin_init_workspace
git clone https://github.com/pal-robotics/gazebo_ros_link_attacher.git
cd ..
catkin_make
source devel/setup.bash
```

## Launch
```bash
roslaunch gazebo_ros_link_attacher test_attacher.launch
```

Empty world with the plugin `libgazebo_ros_link_attacher.so` loaded (in the *worlds* folder).

Which provides the `/link_attacher_node/attach` service to specify two models and their links to be attached.

And `/link_attacher_node/detach` service to specify two models and their links to be detached.

![gazebo screenshot](ss.png)

## Run demo
In another shell, be sure to do `source devel/setup.bash` of your workspace.
```bash
rosrun gazebo_ros_link_attacher spawn.py
```

Three cubes will be spawned.
```bash
rosrun gazebo_ros_link_attacher attach.py
```

The cubes will be attached all between themselves as (1,2), (2,3), (3,1). You can move them with the GUI and you'll see they will move together.
```bash
rosrun gazebo_ros_link_attacher detach.py
```

The cubes will be detached and you can move them separately again.

You can also spawn items with the GUI and run a rosservice call:
```bash
rosservice call /link_attacher_node/attach "model_name_1: 'unit_box_1'
link_name_1: 'link'
model_name_2: 'unit_sphere_1'
link_name_2: 'link'"
```

And same thing to detach:
```bash
rosservice call /link_attacher_node/detach "model_name_1: 'unit_box_1'
link_name_1: 'link'
model_name_2: 'unit_sphere_1'
link_name_2: 'link'"
```
