要在树莓派上控制运行在 PC（Gazebo）上的机器人，利用 ROS 2 的分布式通信特性非常方便。核心思路是：确保两台设备在同一网络下，并设置相同的 ROS_DOMAIN_ID。

以下是具体的操作步骤：

第一步：配置 PC 端 (仿真端)
设置 Domain ID：
在运行 Gazebo 的终端中，设置一个 ID（0-101 之间，例如 5）。

'''
export ROS_DOMAIN_ID=5
'''

启动仿真：
启动您的 Gazebo 仿真环境（假设您已经知道启动命令，例如）：
ros2 launch wpr_simulation2 wpb_home.launch.py


第二步：将代码传输到树莓派
您需要将控制逻辑（home_pkg 功能包）复制到树莓派上编译运行。

在 PC 端打开一个新的终端。
使用 SCP 传输代码：
假设树莓派的用户名是 pi（如果不是请替换），执行以下命令将 home_pkg 复制到树莓派的工作空间（假设树莓派上也有 ~/ros2_ws/src 目录）：

scp -r /home/starfire/ros2_ws/src/home_pkg pi@192.168.137.100:~/ros2_ws/src/


export ROS_DOMAIN_ID=5

cd ~/ros2_ws
colcon build --packages-select home_pkg
source install/setup.bash

在运行节点之前，您可以在树莓派上测试是否能看到 PC 端的话题：


