cmake_minimum_required(VERSION 3.1.3)
project(microprofiler)

# Create user variables
set(MICROPROFILER_LIBRARIES microprofiler CACHE INTERNAL "")

# Set source files
file(GLOB_RECURSE SOURCE_FILES LIST_DIRECTORIES false src/*.cpp)

# Build as static library
add_library(microprofiler ${SOURCE_FILES})

# Add top include directory as public dependency.
# This automatically adds them to parent projects when linking to libut.
target_include_directories(microprofiler PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
	
# Add ut subfolder as private dependency.
# It will thus not be available to parent projects.
target_include_directories(microprofiler PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include/microprofile)

# Require support for at least C++14.
set_property(TARGET microprofiler PROPERTY CXX_STANDARD 14)
set_property(TARGET microprofiler PROPERTY CXX_STANDARD_REQUIRED ON)
