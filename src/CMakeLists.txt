include_directories( 
    ${liquibook_SOURCE_DIR}/include
)

link_directories(
    ${liquibook_SOURCE_DIR}/lib
)


add_library(
    simple_order
    simple_order.cpp
)

add_executable(
    latency_order_book
    latency_order_book.cpp
)

add_executable(
    perf_order_book
    perf_order_book.cpp
)

target_link_libraries(
    latency_order_book
    simple_order
)

target_link_libraries(
    perf_order_book
    simple_order
)
