cmake_minimum_required(VERSION 2.8)
project(publisher)

find_package(rttest REQUIRED)

find_package(opensplice REQUIRED)

# find_package only exposes the c++ include directories but not the c headers
include_directories(c /usr/include/opensplice/dcps/C/SAC ${OPENSPLICE_INCLUDE_DIRS} ${rttest_INCLUDE_DIRS})
link_directories(${OPENSPLICE_LIBRARY_DIRS} ${rttest_LIBRARY_DIR})

add_executable(publisher main.c c/ChatSacDcps.c c/ChatSplDcps.c)
target_link_libraries(publisher ${OPENSPLICE_LIBRARIES})

add_executable(rtt_publisher instrumented_main.c c/ChatSacDcps.c c/ChatSplDcps.c)
target_link_libraries(rtt_publisher ${OPENSPLICE_LIBRARIES} ${rttest_LIBRARIES} m stdc++)
