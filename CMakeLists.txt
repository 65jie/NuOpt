project ("cpp_cmake_gtest_sample")

cmake_minimum_required (VERSION 3.8)
set (CMAKE_CXX_STANDARD 20)
set(CMAKE_DEBUG_POSTFIX _d)

set(PROJECT_VERSION_MAJOR 0)
set(PROJECT_VERSION_MINOR 0)
set(PROJECT_VERSION_PATCH 1)

include_directories(inc)

add_subdirectory ("src")
add_subdirectory("test")
