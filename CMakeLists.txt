cmake_minimum_required(VERSION 2.8.3)
project(static_transform_mux)

find_package(catkin REQUIRED)

catkin_package(
  CATKIN_DEPENDS rospy tf2_msgs
)

install(PROGRAMS
  nodes/static_transform_mux
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)