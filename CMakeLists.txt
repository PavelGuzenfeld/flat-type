cmake_minimum_required(VERSION 3.20)
project(flat-type)

# Require C++23
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(MyLib_FUNCTIONS_DIR "${CMAKE_CURRENT_LIST_DIR}/cmake-library")
list(APPEND CMAKE_MODULE_PATH ${MyLib_FUNCTIONS_DIR})
include(${MyLib_FUNCTIONS_DIR}/library.cmake)

# Find dependencies
find_package(fmt REQUIRED)

# executable and linking
add_executable(${PROJECT_NAME}_test test/flat_type_test.cpp)
target_include_directories(${PROJECT_NAME}_test PUBLIC include)
target_link_libraries(${PROJECT_NAME}_test PRIVATE fmt)

set_debug_options(${PROJECT_NAME}_test)
enable_sanitizers(${PROJECT_NAME}_test)

# installation: properly install headers and binaries
install(DIRECTORY ${CMAKE_SOURCE_DIR}/include/ DESTINATION include)
install(TARGETS ${PROJECT_NAME}_test DESTINATION bin)
