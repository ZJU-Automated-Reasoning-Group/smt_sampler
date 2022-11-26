cmake_minimum_required(VERSION 3.5)
project(opt)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -std=c++11")


##### z3
# We use a modified version of z3. Please pass the path of z3 explicitly.
set(Z3_INCLUDES "" CACHE FILEPATH "Path to your z3 includes")
include_directories(${Z3_INCLUDES}/src/api/c++)
include_directories(${Z3_INCLUDES}/src/api)

if(APPLE)
    set(Z3_LIB ${Z3_INCLUDES}/build/libz3.dylib)
endif()

if(UNIX AND NOT APPLE)
    set(Z3_LIB ${Z3_INCLUDES}/build/libz3.so)
endif()

set(SOURCE_FILES
        smtsampler.cpp
        )

add_executable(samp ${SOURCE_FILES})
target_link_libraries(samp
        ${Z3_LIB}
        )
