
if (DEFINED FIXTURE_ENABLED)

    # add fuzzy test
    file(GLOB_RECURSE fuzzy_files
        # FIXTURE_ENABLED
        main_core.c
        test_election.c
        test_liveness.c
        test_membership.c
        test_replication.c
        )

    add_executable(fuzzy_test ${fuzzy_files})
    set_target_properties(fuzzy_test PROPERTIES OUTPUT_NAME core)
    target_link_libraries(fuzzy_test test_lib craft_static)

endif ()
