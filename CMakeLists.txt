cmake_minimum_required(VERSION 3.0.2)
project(acer_control)

find_package(catkin REQUIRED COMPONENTS
  autoware_msgs
  roscpp
  std_msgs
)

catkin_package(
  CATKIN_DEPENDS autoware_msgs roscpp std_msgs
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

add_executable(acer_vehicle_control
  nodes/acer_vehicle_control/main.cpp
  nodes/acer_vehicle_control/can_cmd_sender.cpp
  nodes/acer_vehicle_control/can_info_receiver.cpp
  nodes/acer_vehicle_control/drv.cpp)
target_link_libraries(acer_vehicle_control ${catkin_LIBRARIES})
if(EXISTS "/usr/include/canlib.h")
target_link_libraries(acer_vehicle_control canlib)
add_definitions(-DUSE_CANLIB)
message("'canlib is installed. Build kvaser.")
endif()
add_dependencies(acer_vehicle_control
  ${catkin_EXPORTED_TARGETS}
)