FROM osrf/ros:humble-desktop

# Example of installing programs
RUN apt-get update \
    && apt-get install -y \
    nano \
    vim \
    ros-${ROS_DISTRO}-gazebo-* \
    && rm -rf /var/lib/apt/lists/*

# Create a non-root user
ARG USERNAME=carver
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
  && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && mkdir /home/$USERNAME/.config && chown $USER_UID:$USER_GID /home/$USERNAME/.config

# Set up sudo
RUN apt-get update \
  && apt-get install -y sudo \
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
  && chmod 0440 /etc/sudoers.d/$USERNAME \
  && rm -rf /var/lib/apt/lists/*

# To add the brashrc
COPY bashrc /home/${USERNAME}/.bashrc

# Set up entrypoint and default command
USER $USERNAME
ENTRYPOINT [ "/bin/bash", "-l", "-c" ]
CMD ["bash"]