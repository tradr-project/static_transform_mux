cmake_minimum_required(VERSION 3.10.2)
project(static_transform_mux)

find_package(catkin REQUIRED)

catkin_package(
  CATKIN_DEPENDS rospy tf2_msgs
)

catkin_install_python(PROGRAMS
  nodes/static_transform_mux
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
