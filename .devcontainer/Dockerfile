FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# 先不改源，先安装 ca-certificates
RUN apt update && apt install -y --no-install-recommends \
    ca-certificates \
    tzdata \
    curl \
    wget \
    gnupg2 \
    lsb-release \
    locales \
    build-essential \
    python3-pip \
    git && \
    rm -rf /var/lib/apt/lists/*

# 替换为阿里云源（注意：只换 http，阿里云的 https 有时不稳定）
RUN sed -i 's|http://.*.ubuntu.com|http://mirrors.aliyun.com|g' /etc/apt/sources.list

# 设置时区为上海
RUN ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    dpkg-reconfigure --frontend noninteractive tzdata

# 设定中文 UTF-8 避免乱码
RUN locale-gen zh_CN.UTF-8 && update-locale LANG=zh_CN.UTF-8

# 添加 ROS 软件源（官方源或者中科大镜像）
RUN echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list && \
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -

# 安装 rosdep 及其依赖
RUN apt update && apt install -y --no-install-recommends \
    python3-rosdep

# 初始化 rosdep（避免 postCreateCommand 失败）
RUN rosdep init || true

SHELL ["/bin/bash", "-c"]
