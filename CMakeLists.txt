cmake_minimum_required(VERSION 3.5)
project(lidar_filter)

# Default to C++17
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
endif()

# Find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(sensor_msgs REQUIRED)

# Include directories
include_directories(
  include
)

# Build the library (optional if you want to link as a library)
add_library(lidar_filter_lib
  src/lidar_filter.cpp
)
ament_target_dependencies(lidar_filter_lib rclcpp sensor_msgs)

# Build the executable
add_executable(lidar_filter_node
  src/main.cpp
)
target_link_libraries(lidar_filter_node lidar_filter_lib)
ament_target_dependencies(lidar_filter_node rclcpp sensor_msgs)

# Install
install(TARGETS
  lidar_filter_node
  DESTINATION lib/${PROJECT_NAME}
)

install(DIRECTORY include/
  DESTINATION include/
)

ament_package()
