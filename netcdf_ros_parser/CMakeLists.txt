cmake_minimum_required(VERSION 2.8.3)
project(netcdf_ros_parser)

find_package(catkin REQUIRED)

catkin_python_setup()

catkin_package(
 CATKIN_DEPENDS
   std_msgs
   geometry_msgs
   geographic_msgs
   nav_msgs
   sensor_msgs
   rospy
   rostopic
   rosgraph
   roslib
   netcdf_ros_msgs
)

catkin_install_python(PROGRAMS scripts/nc_data_server
                               scripts/generate_nc_test_data
                               scripts/print_netcdf_file_info
                      DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

install(DIRECTORY launch files
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
        PATTERN "*~" EXCLUDE)
