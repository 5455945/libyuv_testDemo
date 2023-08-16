cmake_minimum_required(VERSION 3.9)
# mkdir build && cd build
# cmake -G"Unix Makefiles" -S .. -B .
# cmake --build .
# ./yuyv2i420.exe
# ./yuv2rgb.exe

project(yuv_scale)

set(yuyv2i420 "yuyv2i420")
set(yuv2rgb "yuv2rgb")

#set(CMAKE_CXX_STANDARD 11)

set(CMAKE_C_FLAGS "-m64")
set(CMAKE_CXX_FLAGS "-std=c++11 -m64")
#set(CMAKE_C_FLAGS "-m32")
#set(CMAKE_CXX_FLAGS "-std=c++11 -m32")

# on msys2/mingw64
# vim ~/bashrc
# export PATH=.:/wingw64/bin:/wingw64/lib:$PATH

#set(LIB_DIR "/mingw64/lib")
#link_directories(${LIB_DIR})

#-DCMAKE_GENERATOR_PLATFORM=x64

#SET(ROOT_DIR ${CMAKE_SOURCE_DIR})
#message("opencv libs : ", ${CMAKE_SOURCE_DIR})

# pacman -S mingw-w64-x86_64-opencv
# pkg-config --cflags opencv
# pacman -S mingw-w64-x86_64-libyuv
# pacman -S mingw-w64-x86_64-libjpeg-turbo
# pacman -S mingw-w64-x86_64-qt6
# pacman -S mingw-w64-x86_64-qt-creator
# pacman -S mingw-w64-x86_64-qt-creator-devel
# pacman -S mingw-w64-x86_64-qt-creator-docs
# pacman -S mingw-w64-x86_64-qt-installer-framework
# DCMAKE_ARCHITECTURES=x86_64


# 添加opencv includes 路径和库
#set(OpenCV_DIR ${CMAKE_SOURCE_DIR}/opencv45/x86/lib/cmake/opencv4)
set(OpenCV_DIR /mingw64/lib/cmake/opencv4)
#set(OpenCV_INCLUDE_DIRS ${CMAKE_SOURCE_DIR}/opencv45/x86/include/opencv4)
#set(OpenCV_LIBRARIES ${CMAKE_SOURCE_DIR}/opencv45/x86/lib)
#list(APPEND CMAKE_PREFIX_PATH ${CMAKE_SOURCE_DIR}/opencv45/x86)
find_package(OpenCV REQUIRED)
#include_directories(${OpenCV_INCLUDE_DIRS})
#link_directories(${OpenCV_LIBRARIES})


set(libyuv_DIR /mingw64/lib)
#message("opencv libs : ", ${OpenCV_LIBS})

# libyuv
#set(libyuv_DIRS ${CMAKE_SOURCE_DIR}/libyuv/x86)

#find_package(libyuv REQUIRED)
#include_directories(${libyuv_DIRS}/include)

#add_library(yuvso STATIC IMPORTED)
#set_target_properties(yuvso PROPERTIES IMPORTED_LOCATION "D:/install/msys64/mingw64/lib/libyuv.a")


# executable
# add_executable(test_yuv_demo yuv2rgb.cpp)
# target_link_libraries(test_yuv_demo yuvso ${OpenCV_LIBS})


# yuy2 to I420
add_executable(${yuyv2i420} yuyv2i420.cpp)
target_link_libraries(${yuyv2i420} D:/install/msys64/mingw64/lib/libyuv.a ${OpenCV_LIBS})

add_executable(${yuv2rgb} yuv2rgb.cpp)
target_link_libraries(${yuv2rgb} D:/install/msys64/mingw64/lib/libyuv.a ${OpenCV_LIBS})

#set (CMAKE_CXX_LINK_EXECUTABLE "${CMAKE_CXX_LINK_EXECUTABLE} -ldl") 

file(COPY ${CMAKE_SOURCE_DIR}/00316_3.yuyv DESTINATION ${CMAKE_CURRENT_BINARY_DIR} FOLLOW_SYMLINK_CHAIN)
file(COPY ${CMAKE_SOURCE_DIR}/img DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/img FOLLOW_SYMLINK_CHAIN)
