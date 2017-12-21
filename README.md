# NetCDF ROS parser

This package includes ROS services and a parser to allow using data extracted
from a NetCDF file (Network Common Data Form) by interpolating the current
position of the vehicle in the arrays or point clouds stored in a `.nc` file.

This allows the use of real or synthetic data sets of large measurement data that
cannot be generated with the simulation in runtime. For more information on the
NetCDF file format and library, visit their [website](https://www.unidata.ucar.edu/software/netcdf/).

This project took advantage of netCDF software developed by UCAR/Unidata (http://doi.org/10.5065/D6H70CW6).

## Purpose of the project

This software is a research prototype, originally developed for the EU ECSEL
Project 662107 [SWARMs](http://swarms.eu/).

The software is not ready for production use. However, the license conditions of the
applicable Open Source licenses allow you to adapt the software to your needs.
Before using it in a safety relevant setting, make sure that the software
fulfills your requirements and adjust it according to any applicable safety
standards (e.g. ISO 26262).

## Requirements

Be sure to have followed the installation instructions for ROS and the setup
instructions for the catkin workspace [here](http://wiki.ros.org/kinetic/Installation/Ubuntu).
Optionally, install the UUV Simulator package as well by following the [package's instructions](https://uuvsimulator.github.io/installation.html).
Before running the package, install the dependencies found in the
[requirements.txt](requirements.txt) file as follows

```
cat requirements.txt | xargs -n 1 -L 1 pip install
```

Other necessary dependencies can be installed as

```
cd ~/catkin_ws
rosdep install --from-paths src --ignore-src --rosdistro=kinetic
```

## Example of usage

To generate an sample of `.nc` data, run

```
rosrun netcdf_ros_parser generate_nc_test_data
```

To run the `nc_data_server`, run the following ROS node

```
roslaunch netcdf_ros_parser playback_nc_data.launch
```

To subscribe a vehicle to the server to extract the data at the vehicle's
current position, use the following

```
roslaunch netcdf_ros_parser subscribe_vehicle.launch
  namespace:=<robot_namespace>
  odometry_topic:=<Odometry or NatSatFix topic>
  using_gps:=false
  odometry_reference_frame:=<enu, ned or wgs84>
```

By doing this, a topic `/<robot_namespace>/nc_data` will be created where a
[`sensor_msgs/PointCloud`](http://docs.ros.org/api/sensor_msgs/html/msg/PointCloud.html) message
is published with the current position of the vehicle (using the reference
frame convention given) with the interpolated variable data stored in each one
of the message channels.

## License

`netcdf_ros` is open-sourced under the Apache-2.0 license. See the
[LICENSE](LICENSE) file for details.
