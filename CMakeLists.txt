cmake_minimum_required(VERSION 3.5)

########################################################################################################################
# Compilation Options                                                                                                  #
########################################################################################################################

# cpp standard
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
# debug symbol
set(CMAKE_CXX_FLAGS "-g")

# target type
set(compilation_options "Debug")
set(CMAKE_BUILD_TYPE ${compilation_options})

########################################################################################################################
# Global Settings                                                                                                      #
########################################################################################################################

set(project_name "GSL")
project(${project_name})

# test target
set(test_name "${project_name}_test")
set(generate_test ON)

########################################################################################################################
# Import lib                                                                                                           #
########################################################################################################################

# include
include_directories(${CMAKE_SOURCE_DIR}/third_party/googletest/include)

# lib
link_directories(${CMAKE_SOURCE_DIR}/third_party/googletest/lib)

# Internal project
include_directories(${CMAKE_SOURCE_DIR}/include)
include_directories(${CMAKE_SOURCE_DIR}/test)


########################################################################################################################
# test target build                                                                                                    #
########################################################################################################################

file(GLOB_RECURSE TEST_SRC "${CMAKE_SOURCE_DIR}/tests/*")
# Exclude specific files
# list(REMOVE_ITEM TEST_SRC "${CMAKE_SOURCE_DIR}/test/base.cpp")

# test dependency
set(test_dependency "-pthread"
        "-lgtest"
        "-lgmock" )

# test target
if (generate_test STREQUAL "ON")
    add_executable(${test_name} ${TEST_SRC})
    target_link_libraries(${test_name} ${test_dependency})
else()
    message(STATUS "CMakeLists.txt error:test target build error")
endif ()
