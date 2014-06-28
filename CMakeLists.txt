cmake_minimum_required (VERSION 2.8)

set(CMAKE_C_COMPILER "gcc")
set(CMAKE_CXX_COMPILER "g++")

project (unixprotege)

set (EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/build/bin)
set (LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/build/lib)

FIND_PACKAGE (OpenMP)

set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")

include_directories ("${PROJECT_SOURCE_DIR}/build/lib")
add_library (libupsys SHARED
	include/upsys.h)

set_target_properties(libupsys PROPERTIES LINKER_LANGUAGE CXX)

include_directories ("${PROJECT_SOURCE_DIR}/include")

add_executable (list_test src/list_test.cpp)
target_link_libraries(list_test libupsys)