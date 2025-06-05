FROM ros:noetic-ros-base

# 安装常用依赖
RUN apt update && apt install -y \
    python3-pip \
    git \
    curl \
    wget \
    lsb-release \
    locales \
    build-essential \
    ros-noetic-turtlebot3* \
    && rm -rf /var/lib/apt/lists/*

# 设置 ROS 环境变量
ENV ROS_DISTRO=noetic
ENV ROS_WORKSPACE=/root/ros_ws
RUN mkdir -p $ROS_WORKSPACE/src

# 初始化 ROS 工作空间
RUN /bin/bash -c "source /opt/ros/noetic/setup.bash && cd $ROS_WORKSPACE && catkin_make"

# 设置默认路径
WORKDIR $ROS_WORKSPACE