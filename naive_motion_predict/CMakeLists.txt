cmake_minimum_required(VERSION 2.8.3)
project(naive_motion_predict)

include(FindPkgConfig)

find_package(autoware_build_flags REQUIRED)

find_package(catkin REQUIRED COMPONENTS
  autoware_msgs
  imm_ukf_pda_track
  roscpp
  sensor_msgs
  tf
)

set(CMAKE_CXX_FLAGS "-O2 -Wall ${CMAKE_CXX_FLAGS}")

catkin_package()

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

#naive_motion_predict
add_executable(naive_motion_predict
  nodes/naive_motion_predict/naive_motion_predict_node.cpp
  nodes/naive_motion_predict/naive_motion_predict.cpp
)

target_link_libraries(naive_motion_predict
  ${catkin_LIBRARIES}
)

add_dependencies(naive_motion_predict
  ${catkin_EXPORTED_TARGETS}
)

install(
  TARGETS naive_motion_predict
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
  PATTERN ".svn" EXCLUDE
)
