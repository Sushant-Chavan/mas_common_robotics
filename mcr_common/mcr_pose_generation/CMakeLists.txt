cmake_minimum_required(VERSION 2.8.3)
project(mcr_pose_generation)

find_package(catkin REQUIRED
  COMPONENTS
    rospy
    roslint
    tf
)

catkin_python_setup()

catkin_package(
  CATKIN_DEPENDS
    rospy
    std_msgs
    geometry_msgs
    mcr_manipulation_msgs
    tf
)


### TESTS
roslint_python(
  ros/scripts/sampling_parameter_gui_node
)

if(CATKIN_ENABLE_TESTING)
  find_package(roslaunch REQUIRED)
  find_package(rostest REQUIRED)

  roslaunch_add_file_check(ros/launch)
  catkin_add_nosetests(ros/test/pose_generator_unittest.py)
  catkin_add_nosetests(common/test/transformation_unit_test.py)
endif()

install(PROGRAMS
  ros/scripts/sampling_parameter_gui_node
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
