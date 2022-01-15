cmake_minimum_required(VERSION 3.0)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

project(craft)

set(cmake_find_library_suffixes .a)
find_package(LibUV REQUIRED)
if (LibUV_FOUND)
    set(UV_ENABLED True)
endif ()
message(STATUS "LibUV found: ${LibUV_FOUND}")
message(STATUS "LibUV library: ${LibUV_LIBRARY}")

find_package(LZ4 REQUIRED)

add_subdirectory(src)

add_subdirectory(example)

enable_testing()
add_subdirectory(test)
