cmake_minimum_required(VERSION 3.28)
project(demo CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_STANDARD 26)
set(CMAKE_CXX_EXTENSIONS ON)
set(CMAKE_CXX_STANDARD_REQUIRED True)
add_compile_options(-pedantic -Wall -Wextra -stdlib=libstdc++)

# Use GCC standard library from GCC 14.0.0
include_directories(BEFORE SYSTEM "/usr/local/include/c++/14.0.0")
if(${TARGET_ARCH} STREQUAL "x64")
include_directories(BEFORE SYSTEM "/usr/local/include/c++/14.0.0/x86_64-linux-gnu/")
else()
include_directories(BEFORE SYSTEM "/usr/local/include/c++/14.0.0/arm64-linux-gnu/")
endif()

add_library(input)
target_sources(input PUBLIC FILE_SET CXX_MODULES FILES input.cc)
add_library(part_one)
target_sources(part_one PUBLIC FILE_SET CXX_MODULES FILES part_one.cc)
add_library(part_two)
target_sources(part_two PUBLIC FILE_SET CXX_MODULES FILES part_two.cc)

add_executable(demo main.cpp)
target_link_libraries(demo input part_one part_two)