FROM ros:foxy 

RUN mkdir -p uros_ws
WORKDIR uros_ws
RUN git clone --depth 1 -branch -b foxy https://github.com/micro-ROS/micro-ros-build.git src/micro-ros-build \
&&  . /opt/ros/$ROS_DISTRO/setup.sh \
&&  apt update \
&&  apt install ed \
&&  rosdep update \
&&  rosdep install --from-paths src --ignore-src -y \
&&  colcon build \
&&  rm -rf log/ build/ src/* \
&&  rm -rf /var/lib/apt/lists/*

COPY ./micro-ros_entrypoint.sh /micro-ros_entrypoint.sh

RUN echo ". /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc
RUN echo ". /uros_ws/install/setup.bash" >> ~/.bashrc

ENTRYPOINT ["/micro-ros_entrypoint.sh"]
CMD ["bash"]
