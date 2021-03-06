cmake_minimum_required(VERSION 2.8.3)
project(uv_face_detect)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  geometry_msgs
  uv_msgs
  sensor_msgs
  cv_bridge
  message_generation
  image_transport
)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)

#OPEN CV libraries
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
include_directories(/usr/local/share/opencv/haarcascade/)
link_directories(${OpenCV_LIBRARY_DIRS})
set (LIBS ${LIBS} ${OpenCV_LIBS})

#GLUT libraries
#find_package(GLUT REQUIRED)
#find_package(OpenGL REQUIRED)
#include_directories(${GLUT_INCLUDE_DIRS})
#link_directories(${GLUT_LIBRARY_DIRS})
#add_definitions(${GLUT_DEFINITIONS})

#DIA libraries (cvUV)
include_directories(/usr/local/uv_libs/include)
link_directories(/usr/local/uv_libs/lib)
set(UV_LIBS cvDia)
set(LIBS ${UV_LIBS} ${LIBS})

#include_directories(/opt/ros/kinetic/include)
#include_directories(/home/robert/ros_workspace/devel/include/uv_msgs)

## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

################################################
## Declare ROS messages, services and actions ##
################################################

## To declare and build messages, services or actions from within this
## package, follow these steps:
## * Let MSG_DEP_SET be the set of packages whose message types you use in
##   your messages/services/actions (e.g. std_msgs, actionlib_msgs, ...).
## * In the file package.xml:
##   * add a build_depend and a run_depend tag for each package in MSG_DEP_SET
##   * If MSG_DEP_SET isn't empty the following dependencies might have been
##     pulled in transitively but can be declared for certainty nonetheless:
##     * add a build_depend tag for "message_generation"
##     * add a run_depend tag for "message_runtime"
## * In this file (CMakeLists.txt):
##   * add "message_generation" and every package in MSG_DEP_SET to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * add "message_runtime" and every package in MSG_DEP_SET to
##     catkin_package(CATKIN_DEPENDS ...)
##   * uncomment the add_*_files sections below as needed
##     and list every .msg/.srv/.action file to be processed
##   * uncomment the generate_messages entry below
##   * add every package in MSG_DEP_SET to generate_messages(DEPENDENCIES ...)

## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   bBox.msg
#   FaceDetected.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )
#generate_dynamic_reconfigure_options( cfg/pkg_parameters.cfg) 
#include_directories() 
#gencfg()
## Generate added messages and services with any dependencies listed here
#generate_messages(
#   DEPENDENCIES
#   std_msgs  # Or other packages containing msgs
#   geometry_msgs
#   uv_face_detect
# )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#INCLUDE_DIRS include
#  LIBRARIES uv_face_detect
CATKIN_DEPENDS roscpp rospy std_msgs uv_msgs sensor_msgs message_runtime
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)
include_directories(
  ${catkin_INCLUDE_DIRS}
#  ${dynamic_reconfigure_PACKAGE_PATH}/cmake/cfgbuild.cmake
)

## Declare a cpp library
# add_library(uv_face_detect
#   src/${PROJECT_NAME}/uv_face_detect.cpp
# )

## Declare a cpp executable
#add_executable(uv_glip_face_detect src/uv_glip_face_detect.cpp)
add_executable(uv_face_detect src/uv_face_detect.cpp)

#add_executable(uv_3DfaceSegment src/uv_3DFaceSegment.cpp)
## Add cmake target dependencies of the executable/library
## as an example, message headers may need to be generated before nodes
#add_dependencies(uv_face_detect uv_face_detect_gencfg)

## Specify libraries to link a library or executable target against
#target_link_libraries(uv_glip_face_detect
#  ${catkin_LIBRARIES} ${LIBS} ${GLUT_LIBRARY} ${OPENGL_LIBRARY} m 
#)

target_link_libraries(uv_face_detect
  ${catkin_LIBRARIES} ${LIBS} 
)
#target_link_libraries(uv_3DfaceSegment
#   ${catkin_LIBRARIES} ${LIBS} m 
#)


#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS uv_face_detect uv_face_detect_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_uv_face_detect.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
