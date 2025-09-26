# Omron Base package

To view the original Readme.md [click here](./docs/original_readme.md)

This package is a restructuring of [OmronAPAC/Omron_AMR_ROS2](https://github.com/OmronAPAC/Omron_AMR_ROS2)

View [Developer's Guide](https://github.com/guanyewtan/Omron_LD/blob/master/docs/DeveloperGuide.adoc).

## Setup

Create a workspace

```sh
mkdir -p omron_ws/src
cd omron_ws/src
```

Install dependencies
```sh
sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup ros-humble-slam-toolbox
```

Clone the repositories into the `src` folder by

```sh
git clone https://github.com/CollaborativeRoboticsLab/omron_base.git
```

Build by

```sh
cd ..
colcon build
```

## Usage 

### Initialization

1. [Startup TMFLow software with a listener node](https://github.com/CollaborativeRoboticsLab/tmr_ros2?tab=readme-ov-file#-tmflow-listen-node-setup)

2. [Establish Remote connection to TM Robot](https://github.com/CollaborativeRoboticsLab/tmr_ros2?tab=readme-ov-file#-remote-connection-to-tm-robot)

3. Once the robot starts up, it needs to have the listner node loaded (via TMFlow) and should be in the auto mode. On the arm it needs to flash blue and red, while on the pendent a blue light should appear near letter A.

4. If it is in manual mode (arm blinking green and pendent has a yellow light near letter M), press `M/A` button few seconds until the yellow button near M letter starts blinking and quickly enter the password (+-++-) on the pendent using pendent `+` and `-` keys.

### Start with visualization

Run the following command to visualize robot

```sh
source install/setup.bash
ros2 launch amr_description display.launch.py
```

### TM Robot Arm with Moveit 

TM driver node is included in the tm12x_run_move_group.launch.py file. Replace the `<robot_ip_address>` with actual ip address.
```sh
source install/setup.bash
ros2 launch tm12x_moveit_config tm12x_run_move_group.launch.py robot_ip:=<robot_ip_address>
```

### TM Robot Arm with Moveit (Simulation)

TM driver node is included in the tm12x_run_move_group.launch.py file.
```sh
source install/setup.bash
ros2 launch tm12x_moveit_config tm12x_run_move_group.launch.py
```

### Companion Computer Configuration : TM Robot Arm with Moveit

1. TM driver node is included in the tm12x_run_move_group.launch.py file. To start the headless moveit server, uncomment the following line on the companion computer

    ```yaml
    command:
    - ros2 launch tm12x_moveit_config tm12x_run_move_group_headless.launch.py robot_ip:=<robot_ip_address>
    ```

    and run

    ```sh
    docker compose up
    ```

2. On the remote computer run the following command,
    ```sh
    source install/setup.bash
    ros2 launch tm12x_moveit_config tm12x_run_move_group_visualize.launch.py
    ```

