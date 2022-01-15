
# add test library
add_compile_definitions(MUNIT_TEST_NAME_LEN=60)
file(GLOB_RECURSE lib_files
    fault.c
    fsm.c
    heap.c
    munit.c
    tracer.c
    tcp.c
    # FIXTURE_ENABLED
    #cluster.c
    # UV_ENABLED
    aio.c
    dir.c
    tcp.c
    loop.c
    )
add_library(test_lib ${lib_files})
set_target_properties(test_lib PROPERTIES OUTPUT_NAME test)

if (DEFINED FIXTURE_ENABLED)
    target_sources(test_lib PRIVATE cluster.c)
endif ()
