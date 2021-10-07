cmake_minimum_required(VERSION 3.10)

# set the project name
project(Tutorial VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# add the executable
add_executable(Tutorial tutorial.cxx)

# Tells CMake to use binary dir as a include dir
target_include_directories(Tutorial PUBLIC "${PROJECT_BINARY_DIR}")

# Tells CMake it has to pass variables to TutorialConfig.h.in in order to create TutorialConfig.h
configure_file(TutorialConfig.h.in TutorialConfig.h)


