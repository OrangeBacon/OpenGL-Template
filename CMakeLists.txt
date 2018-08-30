cmake_minimum_required(VERSION 3.11.4)
project(OpenGL)

file(GLOB SOURCES "src/*.cpp")

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
add_subdirectory(vendor/glfw)

include_directories(OpenGL PRIVATE lib/glad/include)

IF(CMAKE_BUILD_TYPE STREQUAL "Release")
IF(MSVC)
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /SUBSYSTEM:WINDOWS")
endif()
endif()

add_executable(OpenGL lib/glad/src/glad.c ${SOURCES})
target_link_libraries(OpenGL glfw)