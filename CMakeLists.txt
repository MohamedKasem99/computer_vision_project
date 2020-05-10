cmake_minimum_required(VERSION 3.0.2)
project(my_pcl_tutorial)

add_compile_options(-std=c++14)
find_package(catkin REQUIRED COMPONENTS
  pcl_conversions
  pcl_ros
  roscpp
  sensor_msgs
)

find_package(PCL 1.7 REQUIRED COMPONENTS io common visualization people)
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES my_pcl_tutorial
 CATKIN_DEPENDS pcl_conversions pcl_ros roscpp sensor_msgs libpcl-all
#  DEPENDS system_lib
)
include_directories(
  BEFORE ${PCL_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
add_executable(people_tracking MACOSX_BUNDLE src/people_tracking.cpp)
SET_TARGET_PROPERTIES(people_tracking PROPERTIES LINK_FLAGS -L${PCL_LIBRARY_DIRS})
target_link_libraries(people_tracking ${catkin_LIBRARIES} ${PCL_LIBRARIES})