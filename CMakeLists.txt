# This source file is part of Atlanti's Corp Game Framework. 

cmake_minimum_required(VERSION 3.12)
project(agf-gl LANGUAGES CXX)

# Globs our files for our library. 

file(GLOB agf-gl-srcs src/*.h src/*.cpp)
file(GLOB agf-gl-heads src/*.h)

# Creates our library.

add_library(agf-gl ${agf-gl-src})
target_include_directories(agf-gl src)

# Adds our AGF Main library.

add_subdirectory(agf)
target_link_libraries(agf-gl PUBLIC agf)

# Builds GLFW along with our library. 

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

add_subdirectory(glfw)

target_link_libraries(agf-gl PUBLIC glfw)

# Also links against glbinding library. 

find_package(glbinding REQUIRED)
find_package(globjects REQUIRED)

target_link_libraries(agf-gl PUBLIC 
	glbinding::glbinding
	glbinding::glbinding-aux
	globjects::globjects
)

# Installs our library right now. 

set(CMAKE_INSTALL_PREFIX agf-gl)
install(TARGETS agf-gl DESTINATION lib)
install(FILES ${agf-gl-heads} DESTINATION include)


