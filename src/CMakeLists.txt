file(GLOB_RECURSE src_files "*.c")
file(GLOB_RECURSE include_files "*.h")

add_compile_definitions(HAVE_LINUX_AIO_ABI_H)

#add static library
add_library(craft_static STATIC ${src_files})
# add shared library
add_library(craft SHARED ${src_files})
