cmake_minimum_required(VERSION 3.6)
project(ED_Lib)

set(CMAKE_CXX_STANDARD 11)

#-------------------------------------------------------------------------------
# CMAKE OPTIONS
#-------------------------------------------------------------------------------
option(PACKAGE_TESTS "Build the tests" OFF)

if (CMAKE_BUILD_TYPE MATCHES Debug)
    add_definitions(-DDEBUG)
endif()

#-------------------------------------------------------------------------------
# EXTERNAL LIBRARIES
#-------------------------------------------------------------------------------
find_package(OpenCV REQUIRED)

#-------------------------------------------------------------------------------
# Build EDLib
#-------------------------------------------------------------------------------
file(GLOB EDLib_SRC src/*.cpp)
add_library(EDLib SHARED ${EDLib_SRC})
target_link_libraries(EDLib ${OpenCV_LIBS})
target_include_directories(EDLib PUBLIC include/ ${OpenCV_INCLUDE_DIRS}/include)

#-------------------------------------------------------------------------------
# Tests
#-------------------------------------------------------------------------------
if(PACKAGE_TESTS)
    add_subdirectory(tests)
endif()
