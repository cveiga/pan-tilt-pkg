cmake_minimum_required(VERSION 2.8.3)
project(pan_tilt_camera_teleop)

find_package(catkin REQUIRED COMPONENTS roscpp sensor_msgs geometry_msgs mar_perception)
find_package(VISP REQUIRED)

catkin_package(
  INCLUDE_DIRS
    include 
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS
    roscpp
    sensor_msgs
    geometry_msgs
    mar_perception
  DEPENDS
    VISP
)
include_directories(include ${catkin_INCLUDE_DIRS})

add_executable(keyboard src/keyboard.cpp src/PanTiltController.cpp)
add_executable(keyboardToTopic src/keyboardToTopic.cpp src/PanTiltController.cpp)
add_executable(listener src/main.cpp src/PanTiltController.cpp)
add_executable(vs src/esm_vs_2d.cpp src/PanTiltController.cpp)

target_link_libraries(keyboard ${catkin_LIBRARIES})
target_link_libraries(keyboardToTopic ${catkin_LIBRARIES})
target_link_libraries(listener ${catkin_LIBRARIES})
target_link_libraries(vs ${catkin_LIBRARIES})


add_library(${PROJECT_NAME} 
src/PanTiltController.cpp
)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})# ${PCL_LIBRARIES} ${OpenCV_INCLUDE_DIRS})


