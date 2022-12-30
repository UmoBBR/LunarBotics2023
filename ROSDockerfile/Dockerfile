FROM ros:foxy-ros-core-focal

# Global PATH 
ENV PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100 \
    VENV_PATH=/opt/venv  \
    ROS_DOMAIN_ID=4 \
    ROS_DISTRO=foxy \
    POETRY_PATH=/opt/poetry \
    VENV_PATH=/opt/venv \
    POETRY_VERSION=0.12.17 \
    ROS2_WS=/opt/ros2_ws \
    PATH="/opt/poetry/bin:$PATH" \
    LC_ALL=C.UTF-8 \
    LANG=C.UTF-8

# install bootstrap tools
RUN apt-get update && apt-get install --no-install-recommends -y \
    build-essential \
    curl \
    git \
    python3-colcon-common-extensions \
    python3-colcon-mixin \
    python3-rosdep \
    python3-vcstool \
    python3-pip \
    python3-argcomplete \
    python3.8-venv \
    && rm -rf /var/lib/apt/lists/*

# bootstrap rosdep
RUN rosdep init && \
    rosdep update --rosdistro $ROS_DISTRO

# setup colcon mixin and metadata
RUN colcon mixin add default \
      https://raw.githubusercontent.com/colcon/colcon-mixin-repository/master/index.yaml && \
    colcon mixin update && \
    colcon metadata add default \
      https://raw.githubusercontent.com/colcon/colcon-metadata-repository/master/index.yaml && \
    colcon metadata update

# install ros2 packages
RUN apt-get update &&  apt-get install -y --no-install-recommends \
    ros-foxy-ros-base=0.9.2-1* \
    ros-foxy-desktop \
    && rm -rf /var/lib/apt/lists/*
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y ros-foxy-desktop

# install Poetry
RUN curl -sSL https://install.python-poetry.org | POETRY_HOME=/opt/poetry python3 - \
    && poetry --version \
    && python3 -m venv $VENV_PATH \
    && poetry config settings.virtualenvs.create false \
    && rm -rf /var/lib/apt/lists/*

# setup workspace
RUN mkdir -p $ROS2_WS/code \
    && mkdir $ROS2_WS/Lepton
WORKDIR $ROS2_WS
RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> /root/.bashrc 

ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["bash"]