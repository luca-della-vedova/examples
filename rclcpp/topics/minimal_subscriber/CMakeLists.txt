cmake_minimum_required(VERSION 3.5)
project(examples_rclcpp_minimal_subscriber)

# Default to C++17
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_components REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(map_msgs REQUIRED)

add_executable(subscriber_lambda lambda.cpp)

# This takes 30 seconds to link
target_link_libraries(subscriber_lambda
  rclcpp::rclcpp
  ${std_msgs_LIBRARIES}
  ${geometry_msgs_LIBRARIES}
  ${map_msgs_LIBRARIES}
  )

# This takes < 1 second to link
#ament_target_dependencies(subscriber_lambda rclcpp std_msgs geometry_msgs map_msgs)

install(TARGETS
  subscriber_lambda
  DESTINATION lib/${PROJECT_NAME})

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
