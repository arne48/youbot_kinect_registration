cmake_minimum_required(VERSION 2.8.3)
project(youbot_kinect_registration)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
  std_srvs
  geometry_msgs
  tf
  pcl_ros
  brics_actuator
  sensor_msgs
  cv_bridge
)
find_package(Boost REQUIRED COMPONENTS thread date_time filesystem system)

catkin_package(
  CATKIN_DEPENDS roscpp
)

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/external/cmake_modules)
find_package(Eigen REQUIRED)
include_directories(${catkin_INCLUDE_DIRS} ${Eigen_INCLUDE_DIRS} ${pcl_ros_INCLUDE_DIRS} ${Boost_INCLUDE_DIR})


add_executable(registration src/registration.cpp)
add_dependencies(registration brics_actuator_generate_messages_cpp)
 target_link_libraries(registration
   ${catkin_LIBRARIES}
   ${Boost_LIBRARIES}
 )

add_executable(youbot_kinect_registration src/youbot_kinect_registration.cpp)
add_dependencies(youbot_kinect_registration brics_actuator_generate_messages_cpp)
 target_link_libraries(youbot_kinect_registration
   ${catkin_LIBRARIES}
   ${Boost_LIBRARIES}
 )

add_executable(pattern_detection_test src/pattern_detection_test.cpp)
add_dependencies(pattern_detection_test brics_actuator_generate_messages_cpp)
 target_link_libraries(pattern_detection_test
   ${catkin_LIBRARIES}
 )
