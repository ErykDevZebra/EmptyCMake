cmake_minimum_required(VERSION 3.22)

project(ProjectName)
#include(../headers/CMakeLists.txt)


# Specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Specify the source directory

# Define the executable name
set(EXECUTABLE_FILE MyExecutable)

set(SRC_DIR "../sources")
set(HEAD_DIR "../headers")

# Collect all .cpp files in the src directory
file(GLOB_RECURSE SRC_FILES "${SRC_DIR}/*.cpp")

# Optionally, include header files for IDEs
file(GLOB_RECURSE HEADER_FILES 
    "${HEAD_DIR}/*.h"
    "${HEAD_DIR}/*.hpp"
    )
    
foreach(header_file ${HEADER_FILES})
    message(STATUS "Found header file: ${header_file}")
endforeach()

foreach(src_file ${SRC_FILES})
    message(STATUS "Found source file: ${src_file}")
endforeach()

# Add an executable with all the source files
add_executable(${EXECUTABLE_FILE} ${SRC_FILES} ${HEADER_FILES})

# Optionally, include directories (e.g., for headers)
target_include_directories(${EXECUTABLE_FILE} PRIVATE ${SRC_DIR})

# Add additional libraries, if needed
# target_link_libraries(${EXECUTABLE_FILE} PRIVATE SomeLibrary)

# Add a custom target for cleaning up
add_custom_target(clear
    COMMENT "${CMAKE_BINARY_DIR}"
    COMMAND ${CMAKE_COMMAND} -E remove_directory "${CMAKE_BINARY_DIR}/CMakeFiles"
    COMMAND ${CMAKE_COMMAND} -E remove "${CMAKE_BINARY_DIR}/CMakeCache.txt"
    COMMAND ${CMAKE_COMMAND} -E remove "${CMAKE_BINARY_DIR}/cmake_install.cmake"
    COMMAND ${CMAKE_COMMAND} -E remove "${CMAKE_BINARY_DIR}/Makefile"
    COMMAND ${CMAKE_COMMAND} -E remove "${CMAKE_BINARY_DIR}/${EXECUTABLE_FILE}"
    COMMENT "Removing CMake-generated files and the executable"
)