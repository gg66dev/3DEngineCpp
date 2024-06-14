# Copyright (C) 2014 Barry Deeney
# Copyright (C) 2014 Benny Bobaganoosh
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

################
# CMAKE RULES! #
################
# Huge thanks to mxaddict for setting up the CMake build system!

# we need features that are 3.0 >= dependent
cmake_minimum_required(VERSION 3.0)

# lets name the project
project(3DEngineCpp)

# add the -c and -Wall flags
#add_definitions(
#	-c
#	-Wall
#)

if ( CMAKE_BUILD_TYPE STREQUAL "" )
	# CMake defaults to leaving CMAKE_BUILD_TYPE empty. This screws up
	# differentiation between debug and release builds.
	set(
		CMAKE_BUILD_TYPE
			"Debug"
		CACHE STRING
			"Choose the type of build, options are: None (CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) \"Debug\" \"Release\" \"RelWithDebInfo\" \"MinSizeRel\"."
		FORCE
	)
endif ( CMAKE_BUILD_TYPE STREQUAL "" )

#if ( CMAKE_BUILD_TYPE STREQUAL "Release" )
    #add_definitions( -O2 )
    #endif ( CMAKE_BUILD_TYPE STREQUAL "Release" )

# Lets LOAD app our headers!
file(GLOB_RECURSE HDRS ${3DEngineCpp_SOURCE_DIR}/src/*.h)

# Lets LOAD app our sources!
file(GLOB_RECURSE SRCS
	${3DEngineCpp_SOURCE_DIR}/src/*.cpp
	${3DEngineCpp_SOURCE_DIR}/src/*.c
)


#######################################
# LOOK for the packages that we need! #
#######################################

# OpenGL
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})

# GLEW
add_subdirectory(lib/glew-cmake)
include_directories(BEFORE SYSTEM lib/glew-cmake/include)

# SDL2
add_subdirectory(lib/SDL)
include_directories(BEFORE SYSTEM lib/SDL/include)

# ASSIMP
add_subdirectory(lib/assimp)
include_directories(BEFORE SYSTEM lib/assimp/include)

# Define the executable
add_executable(3DEngineCpp ${HDRS} ${SRCS})

# Define the link libraries
target_link_libraries( 3DEngineCpp
    PRIVATE
    ${OPENGL_LIBRARIES}
	libglew_static
    SDL2-static
	assimp
)

