find_package (Boost COMPONENTS system filesystem unit_test_framework REQUIRED)

include_directories (${TEST_SOURCE_DIR}/unit
                     ${Boost_INCLUDE_DIRS}
                     )

add_definitions (-DBOOST_TEST_DYN_LINK)

add_executable(Test_all_or_none ut_all_or_none.cpp)
add_executable(Test_bbo_order_book ut_bbo_order_book.cpp)
add_executable(Test_depth ut_depth.cpp)
add_executable(Test_immediate_or_cancel ut_immediate_or_cancel.cpp)
add_executable(Test_listeners ut_listeners.cpp)
add_executable(Test_market_price ut_market_price.cpp)
add_executable(Test_order_book ut_order_book.cpp)
add_executable(Test_order_book_shared_ptr ut_order_book_shared_ptr.cpp)
add_executable(Test_stop_orders ut_stop_orders.cpp)

target_link_libraries (Test_all_or_none
                       simple_order
                       ${Boost_FILESYSTEM_LIBRARY}
                       ${Boost_SYSTEM_LIBRARY}
                       ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
                       )

target_link_libraries (Test_bbo_order_book
                       simple_order
                       ${Boost_FILESYSTEM_LIBRARY}
                       ${Boost_SYSTEM_LIBRARY}
                       ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
                       )

target_link_libraries (Test_depth
                       simple_order
                       ${Boost_FILESYSTEM_LIBRARY}
                       ${Boost_SYSTEM_LIBRARY}
                       ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
                       )

target_link_libraries (Test_immediate_or_cancel
                       simple_order
                       ${Boost_FILESYSTEM_LIBRARY}
                       ${Boost_SYSTEM_LIBRARY}
                       ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
                       )

target_link_libraries (Test_listeners
                       simple_order
                       ${Boost_FILESYSTEM_LIBRARY}
                       ${Boost_SYSTEM_LIBRARY}
                       ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
                       )

target_link_libraries (Test_market_price
                       simple_order
                       ${Boost_FILESYSTEM_LIBRARY}
                       ${Boost_SYSTEM_LIBRARY}
                       ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
                       )

target_link_libraries (Test_order_book
                       simple_order
                       ${Boost_FILESYSTEM_LIBRARY}
                       ${Boost_SYSTEM_LIBRARY}
                       ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
                       )

target_link_libraries (Test_order_book_shared_ptr
                       simple_order
                       ${Boost_FILESYSTEM_LIBRARY}
                       ${Boost_SYSTEM_LIBRARY}
                       ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
                       )

target_link_libraries (Test_stop_orders
                       simple_order
                       ${Boost_FILESYSTEM_LIBRARY}
                       ${Boost_SYSTEM_LIBRARY}
                       ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
                       )
