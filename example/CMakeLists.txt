# example of raft
file(GLOB_RECURSE example_server_src "server.c")
add_executable(server ${example_server_src})
add_dependencies(server craft craft_static)
target_link_libraries(server craft_static ${LibUV_LIBRARY} ${Lz4_LIBRARY} pthread dl)
message(${LibUV_LIBRARY})

file(GLOB_RECURSE example_cluster_src "cluster.c")
add_executable(cluster ${example_cluster_src})
add_dependencies(cluster server)
