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

#Generate the shared library from the sources
#add_library(exchange SHARED ${SOURCES})

add_executable(
    latency_order_book
    ${liquibook_SOURCE_DIR}/src/simple_order.cpp
    ${liquibook_SOURCE_DIR}/src/latency_order_book.cpp
)

add_executable(
    perf_order_book
    ${liquibook_SOURCE_DIR}/src/simple_order.cpp
    ${liquibook_SOURCE_DIR}/src/perf_order_book.cpp
)

target_link_libraries(
    latency_order_book
)

target_link_libraries(
    perf_order_book
)
