# cmake needs this line
cmake_minimum_required(VERSION 3.1)

# Enable C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

set(PROJECT_NAME anicode)

# 设置默认值
set(TYPE "0" CACHE STRING "Type of the build")

# 根据TYPE的值设置不同的项目名称
if(TYPE STREQUAL "0")
    set(PROJECT_NAME "segment")
elseif(TYPE STREQUAL "1")
    set(PROJECT_NAME "match")
elseif(TYPE STREQUAL "2")
    set(PROJECT_NAME "animate")
else()
    message(FATAL_ERROR "Invalid TYPE value: ${TYPE}")
endif()

# 添加定义，这会创建一个预处理器宏
add_definitions(-DTYPE_VALUE=${TYPE})

# Define project name
project(${PROJECT_NAME})

# Find OpenCV, you may need to set OpenCV_DIR variable
# to the absolute path to the directory containing OpenCVConfig.cmake file
# via the command line or GUI
find_package(OpenCV REQUIRED)

find_package(ZXing REQUIRED)

set(Zxing_INCLUDE_DIRS /usr/local/include)
set(Zxing_LIBS /usr/local/lib/libzxing.a) 

# If the package has been found, several variables will
# be set, you can find the full list with descriptions
# in the OpenCVConfig.cmake file.
# Print some message showing some of them
message(STATUS "OpenCV library status:")
message(STATUS "    config: ${OpenCV_DIR}")
message(STATUS "    version: ${OpenCV_VERSION}")
message(STATUS "    libraries: ${OpenCV_LIBS}")
message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")
message(STATUS "    zxing include path: ${Zxing_INCLUDE_DIRS}")
message(STATUS "    zxing lib include path: ${Zxing_LIBS}")

# Include headers
include_directories( ./ )
include_directories(${Zxing_INCLUDE_DIRS}) # 添加头文件*.h

# Declare the executable target built from your sources
add_executable(${PROJECT_NAME} main.cpp authorCapture.cpp keyframe.cpp utils.cpp viewerCapture.cpp)

# Link your application with OpenCV libraries
target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBS} ${Zxing_LIBS})
