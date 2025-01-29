cmake_minimum_required(VERSION 3.10)

project(ProjectName)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Define the executable name
set(EXECUTABLE_FILE MyExecutable)

set(SRC_DIR "../sources")
set(HEAD_DIR "../headers")

set(SRC_FILES
    ${SRC_DIR}/main.cpp
    #${SRC_DIR}/other.cpp
)

set(HEADER_FILES
    ${HEAD_DIR}/main.h
    #${HEAD_DIR}/other.h
)

include_directories(${HEAD_DIR})

# Add an executable with all the source files
add_executable(${EXECUTABLE_FILE} ${SRC_FILES})

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
