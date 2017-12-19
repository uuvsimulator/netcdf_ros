cmake_minimum_required(VERSION 2.8.3)
project(netcdf_ros_msgs)

find_package(catkin REQUIRED COMPONENTS std_msgs geometry_msgs geographic_msgs message_generation)

add_service_files(
  FILES
    GetNCData.srv
    GetNCVariables.srv
    GetNCVelocity.srv
    SubscribeToNCServer.srv
)

# Generate added messages and services with any dependencies listed here
generate_messages(
  DEPENDENCIES
    std_msgs
    geometry_msgs
    geographic_msgs
)

catkin_package(
  CATKIN_DEPENDS std_msgs geometry_msgs geographic_msgs message_runtime
)
