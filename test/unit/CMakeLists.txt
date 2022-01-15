
file(GLOB_RECURSE unit_files
    ${CMAKE_SOURCE_DIR}/src/byte.c
    ${CMAKE_SOURCE_DIR}/src/compress.c
    ${CMAKE_SOURCE_DIR}/src/configuration.c
    ${CMAKE_SOURCE_DIR}/src/err.c
    ${CMAKE_SOURCE_DIR}/src/heap.c
    ${CMAKE_SOURCE_DIR}/src/log.c
    main_core.c
    test_byte.c
    test_compress.c
    test_configuration.c
    test_err.c
    test_log.c
    test_queue.c
    )

add_executable(unit_tests ${unit_files})
set_target_properties(unit_tests PROPERTIES OUTPUT_NAME core)
target_link_libraries(unit_tests test_lib)

# UV_ENABLED
if (UV_ENABLED)
    add_compile_definitions(HAVE_LINUX_AIO_ABI_H)
    # add unit uv test
    file(GLOB_RECURSE unit_uv_files
        # UV_ENABLED
        ${CMAKE_SOURCE_DIR}/src/err.c
        ${CMAKE_SOURCE_DIR}/src/heap.c
        ${CMAKE_SOURCE_DIR}/src/syscall.c
        ${CMAKE_SOURCE_DIR}/src/tracing.c
        ${CMAKE_SOURCE_DIR}/src/uv_fs.c
        ${CMAKE_SOURCE_DIR}/src/uv_os.c
        ${CMAKE_SOURCE_DIR}/src/uv_writer.c
        main_uv.c
        test_uv_fs.c
        test_uv_writer.c
        )

    add_executable(unit_uv_test ${unit_uv_files})
    set_target_properties(unit_uv_test PROPERTIES OUTPUT_NAME uv)
    target_link_libraries(unit_uv_test test_lib ${LibUV_LIBRARY})

endif ()
