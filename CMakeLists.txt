cmake_minimum_required(VERSION 3.0)
project(ACM_PC)

include_directories(include)

#Can manually add the sources using the set command as follows:
#set(SOURCES src/mainapp.cpp src/Student.cpp)
 
#However, the file(GLOB...) allows for wildcard additions:
file(GLOB SOURCES "src/*.cpp")
file(GLOB HEADERS "include/*.h")

# External library include directories
set(SERIAL_LIBRARY_INCLUDE_DIR "" CACHE STRING "Path to SerialLibrary include directory")
include_directories(${SERIAL_LIBRARY_INCLUDE_DIR})

set(FFTW3_INCLUDE_DIR "" CACHE STRING "Path to FFTW3 include directory")
include_directories(${FFTW3_INCLUDE_DIR})

# External library lib directories
set(SERIAL_LIBRARY_LIB_DIR "" CACHE STRING "Path to SerialLibrary lib directory")
link_directories(${SERIAL_LIBRARY_LIB_DIR})

set(FFTW3_LIB_DIR "" CACHE STRING "Path to FFTW3 lib directory")
link_directories(${FFTW3_LIB_DIR})

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

target_link_libraries(${PROJECT_NAME} debug serial-d.lib optimized serial.lib
	debug libfftw3-3-d.lib optimized libfftw3-3.lib)