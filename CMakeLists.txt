cmake_minimum_required(VERSION 3.2)

project(a6-rigid-bodies-contact)

#Important CMAKE stuff
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
SET(GCC_COVERAGE_COMPILE_FLAGS "-Wa,-mbig-obj")

#setup libigl properly
# libigl
option(LIBIGL_WITH_OPENGL               "Use OpenGL"            ON)
option(LIBIGL_WITH_OPENGL_GLFW          "Use GLFW"              ON)
option(LIBIGL_WITH_OPENGL_GLFW_IMGUI    "Use ImGui"             ON)

find_package(LIBIGL REQUIRED QUIET)

#include directories
include_directories(${PROJECT_SOURCE_DIR}/shared/include)
include_directories(${PROJECT_SOURCE_DIR}/include)
include_directories(${PROJECT_SOURCE_DIR})
include_directories(${LIBIGL_INCLUDE_DIR})

#include source code
file(GLOB H_FILES ${PROJECT_SOURCE_DIR}/include/*.h)
file(GLOB CPP_FILES ${PROJECT_SOURCE_DIR}/src/*.cpp)

#build executable 
add_executable(${PROJECT_NAME} main.cpp .h ${H_FILES}  ${CPP_FILES})
add_definitions(${GCC_COVERAGE_COMPILE_FLAGS})
target_link_libraries(${PROJECT_NAME} igl::core igl::opengl igl::opengl_glfw igl::opengl_glfw_imgui)

