# Set min req version of Cmake
cmake_minimum_required(VERSION 3.16)

# Set the project name
project(mpsse-cli)

# Include the libMPSSE sub-directory
add_subdirectory(libMPSSE)

# Set our include directories
include_directories(inc
                    libMPSSE/inc
                    libMPSSE/inc/linux)

# Set the binary output folder
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/output)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/output)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/output)

set(APP_SRC ${PROJECT_SOURCE_DIR}/src/mpsse-cli.c
            ${PROJECT_SOURCE_DIR}/src/spi.c
)

# Create our executable
add_executable(mpsse-cli ${APP_SRC})

# Link against the MPSSE, dl and ftd2xx libs
target_link_libraries(mpsse-cli MPSSE dl ftd2xx)

# Install the cli app to our bin folder
install(TARGETS mpsse-cli DESTINATION bin)