cmake_minimum_required(VERSION 3.0.2)
project(autorunner)

## Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)

find_package(autoware_msgs REQUIRED)
find_package(catkin REQUIRED)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  autoware_msgs
)

catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES minicar_autorunner
#  CATKIN_DEPENDS other_catkin_pkg
#  DEPENDS system_lib
)

include_directories(
  include ${catkin_INCLUDE_DIRS}
  ${autoware_msgs_INCLUDE_DIRS}
)

add_library(ros_autorunner_lib
  include/ros_autorunner/ros_autorunner_def.h
  include/ros_autorunner/ros_autorunner.h
  src/ros_autorunner/ros_autorunner.cpp
)

add_executable(cubetown_autorunner
  include/cubetown_autorunner/cubetown_autorunner.h
  src/cubetown_autorunner/cubetown_autorunner_node.cpp
  src/cubetown_autorunner/cubetown_autorunner.cpp
)

add_dependencies(cubetown_autorunner ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(cubetown_autorunner
  ${catkin_LIBRARIES}
  ros_autorunner_lib
)