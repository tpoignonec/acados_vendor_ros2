ARG ROS_DISTRO="humble"
FROM ros:${ROS_DISTRO}

COPY . /ros2_dev/src/acados_vendor_ros2
RUN apt update && apt upgrade -y
RUN apt install -y python3-pip
RUN apt install -y git clang-format-14 cppcheck
RUN pip install pre-commit
RUN apt update && \
    cd ros2_dev/src/acados_vendor_ros2 && \
    git submodule update --init --recursive
RUN cd ros2_dev/ && \
    . /opt/ros/${ROS_DISTRO}/setup.sh && \
    rosdep install --ignore-src --from-paths . -y -r
RUN cd ros2_dev/ && \
    . /opt/ros/${ROS_DISTRO}/setup.sh && \
    colcon build --event-handlers console_direct+ && \
    colcon build # Second build for acados_template python lib
# COPY .docker/run/ros_entrypoint.sh /ros_entrypoint.sh
# RUN chmod 755 /ros_entrypoint.sh
# ENTRYPOINT ["ros_entrypoint.sh"]
CMD ["bash"]
