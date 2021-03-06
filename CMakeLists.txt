#
# CMake for MATio
#
cmake_minimum_required (VERSION 2.6.8)

#
# Project Name
#
project (MATio CXX)

OPTION(BUILD_TESTS "Build unit tests" ON)

set (CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -std=c++11 -Wall -Wpedantic")

find_package (Eigen3 REQUIRED)
find_package (Matio REQUIRED)
find_package (HDF5 REQUIRED)

include_directories(include)
include_directories (${EIGEN3_INCLUDE_DIR})
include_directories (${MATIO_INCLUDE_DIRS})

if(BUILD_TESTS)
  enable_testing ()
  add_definitions(-DBOOST_TEST_DYN_LINK)
  find_package(Boost COMPONENTS ${BOOST_COMPONENTS} unit_test_framework REQUIRED)
  add_subdirectory (tests)
endif()

install (DIRECTORY "include/MATio" DESTINATION include)
