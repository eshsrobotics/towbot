PROJECT(towbot CXX)

# Required for add_subdirectory() support.
cmake_minimum_required(VERSION 3.11)

# Build the nested ArUco library.
set(ARUCO_DIRECTORY "./aruco-3.0.10")
include_directories("${ARUCO_DIRECTORY}/src")
add_subdirectory("${ARUCO_DIRECTORY}" ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})
