cmake_minimum_required(VERSION 3.8.0)

project(liquibook)

set(CMAKE_BUILD_TYPE Release)
set (CMAKE_CXX_STANDARD 11)

include_directories( 
    ${liquibook_SOURCE_DIR}/include
)

link_directories(
    ${liquibook_SOURCE_DIR}/lib
)

set(
	CMAKE_CXX_LINK_FLAGS 
)

add_subdirectory(src)
add_subdirectory(test)
enable_testing()
add_test (NAME UnitTests COMMAND LiquibookTest)
