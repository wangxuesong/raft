cmake_minimum_required(VERSION 3.0)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

project(craft)

set(cmake_find_library_suffixes .a)
find_package(LibUV REQUIRED)
message(STATUS "LibUV found: ${LibUV_FOUND}")
message(STATUS "LibUV library: ${LibUV_LIBRARY}")
#FindLz4()
find_package(LZ4 REQUIRED)
#auto_source(libraft_src "*.c" "${CMAKE_CURRENT_SOURCE_DIR}/src")
file(GLOB_RECURSE src_files "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c")
file(GLOB_RECURSE include_files "${CMAKE_CURRENT_SOURCE_DIR}/src/*.h")
# message(STATUS "src_files: ${src_files}")
# message(STATUS "include_files: ${include_files}")

add_compile_definitions(HAVE_LINUX_AIO_ABI_H)

#add static library
add_library(craft_static STATIC ${src_files})
# add shared library
add_library(craft SHARED ${src_files})

# example of raft
file(GLOB_RECURSE example_server_src "${CMAKE_CURRENT_SOURCE_DIR}/example/server.c")
add_executable(server ${example_server_src})
add_dependencies(server craft craft_static)
target_link_libraries(server craft ${LibUV_LIBRARY} ${Lz4_LIBRARY})

file(GLOB_RECURSE example_cluster_src "${CMAKE_CURRENT_SOURCE_DIR}/example/cluster.c")
add_executable(cluster ${example_cluster_src})
add_dependencies(cluster server)
