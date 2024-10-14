cmake_minimum_required(VERSION 3.8)
project(ira_interfaces)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(sensor_msgs REQUIRED)

# Define your custom messages
set(msg_files
  "msg/ArmComplete.msg"
  "msg/GptComplete.msg"
  "msg/SystemState.msg"
  "msg/FoiCoord.msg"
  "msg/CanvasImage.msg"
)

# Define your custom services
set(srv_files
  "srv/ReadyCheck.srv"
)

# Generate interfaces
rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files} 
  DEPENDENCIES sensor_msgs  # Declare sensor_msgs as a dependency here
 )

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
