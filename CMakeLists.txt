cmake_minimum_required(VERSION 2.8.3)
project(openhmd_occulus_touch)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake_modules/")
find_package(catkin REQUIRED COMPONENTS
  sensor_msgs
  tf
)

## System dependencies are found with CMake's conventions
find_package(sdl2 REQUIRED)
find_package(Threads REQUIRED)
find_package(libusb-1.0 REQUIRED)

include_directories(${LIBUSB_1_INCLUDE_DIRS})
include_directories(${SDL2_INCLUDE_DIRS})

catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES openhmd_occulus_touch
#  CATKIN_DEPENDS sensor_msgs tf
#  DEPENDS system_lib
)

include_directories(
 lib
  ${catkin_INCLUDE_DIRS}
)
 MESSAGE("!!!!!!!!!!!!!!!!!!!!!!!!!!! ${LIBUSB_1_LIBRARY}")

 set(lib_hdrs lib/blobwatch.h lib/ar0134.h lib/esp770u.h lib/uvc.h)
 set(lib_srcs lib/ar0134.c lib/blobwatch.c lib/esp770u.c lib/uvc.c)
 #set(lib_srcs lib/ar0134.cpp lib/blobwatch.cpp lib/esp770u.cpp lib/uvc.cpp)
 #add_library(occulus_lib lib/blobwatch.h lib/ar0134.h lib/esp770u.h lib/uvc.h lib/ar0134.c lib/blobwatch.c lib/esp770u.c lib/uvc.c)
 #target_link_libraries(occulus_lib
 #  ${LIBUSB_1_LIBRARY}
 #  SDL2
 # ) 
 add_executable(${PROJECT_NAME}_node src/main.cpp ${lib_hdrs} ${lib_srcs})

 target_link_libraries(${PROJECT_NAME}_node
   ${catkin_LIBRARIES}
   ${LIBUSB_1_LIBRARY}
   SDL2
 )
