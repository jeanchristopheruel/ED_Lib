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
if(PACKAGE_TESTS)
    set(CV_MODULES core imgproc imgcodecs)
else()
    set(CV_MODULES core imgproc)
endif()
find_package(OpenCV 4.0 REQUIRED ${CV_MODULES})

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
