PROJECT(towbot CXX)

# This is the lowest common denominator--lots of distributions should have at
# least this version.
cmake_minimum_required(VERSION 3.0)

# Turn off win32 compilation for Cygwin.  Not doing so emits warnings during
# Windows builds, and we don't need Win32 support anyway.
set(CMAKE_LEGACY_CYGWIN_WIN32 0)

# A nifty trick from https://stackoverflow.com/q/10851247 for forcing the
# compiler to build against the C++11 standard.  It only supports g++ right
# now.
macro(use_cxx11)
  if (CMAKE_VERSION VERSION_LESS "3.1")
    if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
      set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=gnu++11")
    endif ()
  else ()
    set (CMAKE_CXX_STANDARD 11)
  endif ()
endmacro(use_cxx11)

use_cxx11()

# ------------------------------
# Define our output directories.
# ------------------------------
set (MY_EXECUTABLE_DIRECTORY "./bin")
set (MY_LIBRARY_DIRECTORY "./lib")

# -------------------------------
# Build the nested ArUco library.
# -------------------------------
set(ARUCO_DIRECTORY "./aruco-3.0.10")
include_directories("${ARUCO_DIRECTORY}/src") # Allows everyone to #include "aruco.h"
add_subdirectory("${ARUCO_DIRECTORY}")
link_directories("${ARUCO_DIRECTORY}/lib")


# ---------------
# Link to OpenCV.
# ---------------

# ArUco has a hard dependency on OpenCV, so we need to be able to link to it
# and include its headers.
find_package(OpenCV REQUIRED)
if(OPENCV_FOUND)
  message(STATUS "** OpenCV ${OpenCV_VERSION} detected. **" )
endif()
include_directories(${OpenCV_INCLUDE_DIRS})

# ---------------------------------------------------
# Define our source file sets and target directories.
# ---------------------------------------------------
set(TEST_SOURCES "src/main.cpp")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${MY_LIBRARY_DIRECTORY}")    # Dynamic libraries
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${MY_LIBRARY_DIRECTORY}")    # Static libraries
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${MY_EXECUTABLE_DIRECTORY}") # Executables

# --------------------------------------------------------------
# Define our compilation targets (i.e., the final build output.)
# --------------------------------------------------------------
add_executable(camera-test ${TEST_SOURCES})
target_link_libraries(camera-test ${OpenCV_LIBS})
target_link_libraries(camera-test "aruco")
