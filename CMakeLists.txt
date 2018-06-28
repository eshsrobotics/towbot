PROJECT(towbot CXX)

# This is the lowest common denominator--lots of distributions should have at
# least this version.
cmake_minimum_required(VERSION 3.0)

# Build the nested ArUco library.
set(ARUCO_DIRECTORY "./aruco-3.0.10")
include_directories("${ARUCO_DIRECTORY}/src")
add_subdirectory("${ARUCO_DIRECTORY}" ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})
