
if (DEFINED FIXTURE_ENABLED)

    # add integration test
    file(GLOB_RECURSE integration_files
        # FIXTURE_ENABLED
        main_core.c
        test_apply.c
        test_assign.c
        test_barrier.c
        test_bootstrap.c
        test_digest.c
        test_election.c
        test_fixture.c
        test_heap.c
        test_membership.c
        test_recover.c
        test_replication.c
        test_snapshot.c
        test_strerror.c
        test_tick.c
        test_transfer.c
        test_start.c
        )

    add_executable(integration_test ${integration_files})
    set_target_properties(integration_test PROPERTIES OUTPUT_NAME core)
    target_link_libraries(integration_test test_lib craft_static)

endif ()

# UV_ENABLED
if (UV_ENABLED)
    add_compile_definitions(HAVE_LINUX_AIO_ABI_H)
    # add integration test
    file(GLOB_RECURSE integration_uv_files
        # UV_ENABLED
        ${raft_sources}
        main_uv.c
        test_uv_init.c
        test_uv_append.c
        test_uv_bootstrap.c
        test_uv_load.c
        test_uv_recover.c
        test_uv_recv.c
        test_uv_send.c
        test_uv_set_term.c
        test_uv_tcp_connect.c
        test_uv_tcp_listen.c
        test_uv_snapshot_put.c
        test_uv_truncate.c
        )

    add_executable(integration_uv_test ${integration_uv_files})
    set_target_properties(integration_uv_test PROPERTIES OUTPUT_NAME uv)
    target_link_libraries(integration_uv_test test_lib ${LibUV_LIBRARY})

endif ()
