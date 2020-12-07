cmake_minimum_required(VERSION 3.15)
project(TestPod C CXX)

# Download automatically, you can also just copy the conan.cmake file
if(NOT EXISTS "${CMAKE_BINARY_DIR}/conan.cmake")
   message(STATUS "Downloading conan.cmake from https://github.com/conan-io/cmake-conan")
   file(DOWNLOAD "https://github.com/conan-io/cmake-conan/raw/v0.15/conan.cmake"
                 "${CMAKE_BINARY_DIR}/conan.cmake" 
                 TLS_VERIFY ON)
endif()

include(${CMAKE_BINARY_DIR}/conan.cmake)

conan_cmake_run(REQUIRES fmt/6.1.2
                BASIC_SETUP
                CMAKE_TARGETS
                BUILD missing)


add_executable(hello_c main.c)

add_executable(hello_cpp main.cpp)

add_executable(hello_cpp20 main20.cpp)
target_link_libraries(hello_cpp20 CONAN_PKG::fmt)
