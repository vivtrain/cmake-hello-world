# Usage (generate build files):
#   $ cd build/
#   $ cmake ..
# Build (generate target executable)
#   $ cd build/
#   $ make
# Run
#   $ ./bin/hello

# Require a floor for CMake version
cmake_minimum_required(VERSION 3.16)

# Set the prjoect name and explicit
project(cmakeHelloWorld LANGUAGES CXX)

# Define a C++ Standard and enforce it
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Generate compile commands for LSPs
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Put all binaries in build/bin
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# Create a target library
add_library(greet STATIC src/greet.cpp)
set_target_properties(greet PROPERTIES
  ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib/greet
  LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib/greet
)

# Tell CMake where your includes are located
target_include_directories(greet PUBLIC ${PROJECT_SOURCE_DIR}/include/greet)

# Define a target executable + it's sources
add_executable(hello src/main.cpp)

# Link the executable against the target library
target_link_libraries(hello PRIVATE greet)

